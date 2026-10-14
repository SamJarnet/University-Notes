# Annotated Paper Summaries: LLM-Guided Reward Adaptation for RL Satellite Collision Avoidance

Sam Jarnet | Supervisor: Dr. Panayiotis Danassis | Updated with additional papers

*Papers 1-15 are your supervisor/reading-list papers. Papers 16-24 are additional papers I found. Items marked \[CHECK\] could not be verified from the source I accessed and should be confirmed against the full paper. Goals: G1 = RL agent under changing conditions; G2 = reward changes; G3 = LLM translation of changes into rewards; G4 = iterative LLM adaptation vs alternatives.*

## Part A. Original reading list

### Core reward-design papers

**1. Adaptive Reward Design in RL: A Taxonomy and Survey (Baybas, D'Eramo and Brune, IJCAI 2026)**

Link: [ijcai.org/proceedings/2026/863](https://www.ijcai.org/proceedings/2026/863)

Summary: The survey argues that adaptive reward design is scattered across reward shaping, curriculum learning, intrinsic motivation, non-stationary objectives and preference or feedback learning. It organises the field by the driver of reward change: external feedback, endogenous within-run signals, and exogenous context.

For your project: Your LLM loop (simulate, observe, revise) is the external-feedback category, so this gives you the vocabulary for your methodology. A reward conditioned on a mission-priority input is the exogenous-context category and a natural baseline. Use its assignment rules to say precisely what your method is and is not.

**2. Balancing Act: Prioritization Strategies for LLM-Designed Restless Bandit Rewards (Verma et al., 2024) \[CHECK authors\]**

Link: [arxiv.org/abs/2408.12112](https://arxiv.org/abs/2408.12112)

Summary: An LLM proposes candidate rewards from a natural-language priority statement, and a separate adjudicator selects among them using social-choice-style prioritisation. The LLM does not decide the trade-off itself, which reduces over-optimisation of one objective.

For your project: This is the closest match to keeping balanced performance (G3). Copy the generator/selector split: the LLM writes candidates and a fixed rule scores them on collision rate, fuel use and trajectory deviation.

**3. LLM-Driven Automated Reward Design for RL Routing in LEO Satellite Networks, LARGE (Casas, da Fonseca and Astudillo, 2026)**

Link: [arxiv.org/abs/2608.01649](https://arxiv.org/abs/2608.01649)

Summary: LARGE generates an initial reward from the LLM's prior knowledge and refines it with simulator feedback. Reward quality improves within a few iterations, and the best configuration reaches goodput within roughly 3% of an expert baseline with slightly lower delay.

For your project: It is your closest satellite-domain precedent and shows results are mixed across metrics. Mirror its evaluation protocol (iteration counts, expert-reward comparison, several backbones) and expect similar trade-offs between collision rate, fuel and deviation.

**4. Eureka: Human-Level Reward Design via Coding LLMs (Ma et al., 2024)**

Link: [arxiv.org/abs/2310.12931](https://arxiv.org/abs/2310.12931)

Summary: The LLM reads environment source code and writes executable reward code. It samples several candidates per iteration, trains a policy on each, and receives a "reward reflection": an automatic summary of training statistics including each reward component. It outperformed human-designed rewards on most robotics tasks \[CHECK figures\].

For your project: This is your main template for G3 and G4. Log each reward component (collision penalty, fuel cost, deviation cost) separately so the LLM can see which term is exploited or ignored, and use the evolutionary generate-evaluate-reflect loop.

**5. Autonomous Spacecraft Collision Avoidance with a Variable Number of Space Debris Based on Safe RL (Mu et al., 2024)**

Link: [doi.org/10.1016/j.ast.2024.109131](https://doi.org/10.1016/j.ast.2024.109131)

Summary: Uses LSTM networks for adaptive feature extraction so the agent can handle a variable number of debris, and formulates the problem as a constrained MDP solved with the P3O safe-RL algorithm. I could access only the abstract and highlights.

For your project: This is your base formulation: debris representation, safety as a constraint, and performance measures. Read the full text for state, action and reward terms, since those become the original reward your LLM edits. It also raises a design question: may the LLM change the safety constraint, or only the soft terms?

### Environment-design and curriculum papers

**6. PAIRED (Dennis et al., 2020)**

Link: [arxiv.org/abs/2012.02096](https://arxiv.org/abs/2012.02096)

Summary: An adversary designs environments that maximise a protagonist's regret relative to an antagonist, producing challenging but solvable tasks. It beats naive domain randomisation (often too easy) and minimax adversaries (which can produce impossible tasks).

For your project: It explains why you should not simply randomise failures. It also warns that stress tests must stay learnable: some degradations make a collision unavoidable. Regret relative to the best achievable performance is a possible metric.

**7. ACCEL (Parker-Holder et al., 2022)**

Link: [proceedings.mlr.press/v162/parker-holder22a](https://proceedings.mlr.press/v162/parker-holder22a.html)

Summary: Combines prioritised replay of high-regret levels with small mutations of those levels, so complexity emerges gradually where the agent still struggles.

For your project: Use small edits to an existing scenario (add debris, shift the miss distance, reduce thrust by 10%) to build graded degradation conditions for G1. It is also a candidate comparison baseline for G4.

**8. EnvGen (Zala et al., 2024)**

Link: [arxiv.org/abs/2403.12014](https://arxiv.org/abs/2403.12014)

Summary: An LLM generates environment configurations, a small RL agent trains in them for short cycles interleaved with the original environment, and the LLM receives a report of the agent's weaknesses to propose new environments.

For your project: The most direct alternative to reward adaptation: adapt the training environment instead of the reward. It makes a strong baseline for G4, and its feedback report format is reusable.

**9. Eurekaverse (Liang et al., 2025)**

Link: [proceedings.mlr.press/v270/liang25a](https://proceedings.mlr.press/v270/liang25a.html)

Summary: An LLM writes terrain code for quadruped parkour and an evolutionary loop selects environments that improve the policy, with attention to keeping tasks learnable. It transferred to a real robot \[CHECK\].

For your project: The same loop could generate debris encounter geometries or failure profiles. Add a feasibility check that rejects scenarios with no safe action.

### Pipeline efficiency and grounding

**10. CARD (Sun et al., 2024) \[CHECK authors\]**

Link: [arxiv.org/abs/2410.14660](https://arxiv.org/abs/2410.14660)

Summary: A Coder LLM writes reward code and an Evaluator LLM gives feedback. A trajectory-preference evaluation checks whether a candidate reward ranks trajectories consistently with a task-success measure, reducing full training runs.

For your project: RL training will likely be your bottleneck. A cheap preference check (does this reward rank a collision trajectory below a safe one?) can filter candidates before training and catches rewards that reward the wrong thing.

**11. Text2Reward (Xie et al., 2024)**

Link: [arxiv.org/abs/2309.11489](https://arxiv.org/abs/2309.11489)

Summary: Given a natural-language goal and a compact code-style description of the environment, an LLM generates dense executable reward code, with optional human-feedback refinement. It matched or approached expert rewards on many manipulation tasks \[CHECK\].

For your project: Best reference for G3: turning "raise altitude by 20 km, prioritise fuel" into reward code. Give the LLM a structured abstraction (classes and fields for orbit state, debris, fuel) rather than raw simulator code. A one-shot no-feedback version is a useful baseline.

**12. Reward-Conditioned RL, RCRL (Nauman, Cygan and Abbeel, 2026)**

Link: [arxiv.org/abs/2603.05066](https://arxiv.org/abs/2603.05066)

Summary: Conditions the agent on reward parameters while collecting experience under a single nominal reward, relabelling stored experience with counterfactual rewards. It reports efficient adaptation to new parameterisations and zero-shot behavioural adjustment at deployment.

For your project: Your best non-LLM alternative for G4: condition on weights for collision, fuel and deviation and shift them at deployment without retraining. A hybrid is possible: the LLM picks the parameters and a conditioned policy executes them. Check whether this fits your fixed-architecture scope.

### Theory and domain grounding

**13. Policy Invariance under Reward Transformations (Ng, Harada and Russell, 1999)**

Link: [ai.stanford.edu/\~ang/papers/shaping-icml99.pdf](https://ai.stanford.edu/~ang/papers/shaping-icml99.pdf)

Summary: Potential-based shaping, F = γΦ(s') − Φ(s), is the class of additive shaping guaranteed to preserve the optimal policy. Other modifications can change what is optimal.

For your project: A principled way to classify LLM edits: pure shaping speeds learning without changing the goal, while re-weighting or adding terms deliberately changes it, as a mission change requires. It also underpins a safe-edit validator and your discussion of reward hacking.

**14. NASA CARA guidance**

Link: [nasa.gov/cara](https://www.nasa.gov/cara/)

Summary: Describes operational conjunction assessment: screening close approaches, characterising uncertainty with covariance, computing probability of collision (Pc) and miss distance, and deciding when to manoeuvre against risk thresholds.

For your project: Grounds your metrics (use Pc and miss distance, not just collided or not), informs how to model degraded sensing, and gives realistic risk thresholds. Check the site for the current values.

**15. Curriculum Learning for RL Domains (Narvekar et al., 2020)**

Link: [jmlr.org/beta/papers/v21/20-212](https://jmlr.org/beta/papers/v21/20-212.html)

Summary: Formalises curricula as task generation, sequencing and transfer, and surveys evaluation measures such as time to threshold, jumpstart and asymptotic performance.

For your project: Use its measures to compare adaptation methods (fine-tune on the new reward, retrain from scratch, LLM-adapted reward) and to choose a fair curriculum baseline.

## Part B. Additional papers

### LLM reward design

**16. Language to Rewards for Robotic Skill Synthesis (Yu et al., CoRL 2023)**

Link: [arxiv.org/abs/2306.08647](https://arxiv.org/abs/2306.08647)

Summary: Argues that reward functions are a better interface between language and low-level control than raw actions. A Reward Translator LLM maps natural-language instructions to reward-specifying code, and an optimiser (MuJoCo MPC) finds the actions. Users can give corrections and see results immediately. It was evaluated on 17 simulated tasks for a quadruped and a dexterous manipulator.

For your project: It is the clearest early argument for G3, that reward code is the right interface for translating a mission change. The correction-in-language loop is a useful comparison to your simulator-feedback loop, and the paper is an easy citation for the idea of reward as an intermediate representation.

**17. The Evolving Landscape of LLM- and VLM-Integrated RL (survey, arXiv 2502.15214) \[CHECK authors\]**

Link: [arxiv.org/abs/2502.15214](https://arxiv.org/abs/2502.15214)

Summary: Surveys how LLMs and VLMs are integrated into RL, with a section on reward design. It notes that approaches differ mainly in how refinements are triggered and what kind of language feedback is used, and that Text2Reward, Eureka and similar methods reach or exceed expert-designed rewards while needing little human effort.

For your project: Use it to place your work within the wider LLM-for-RL taxonomy and to find further citations. It complements the Baybas et al. taxonomy, which is organised by what drives the reward change, with a view organised by the LLM's role.

**18. MAESTRO: Multi-Agent Environment Shaping through Task and Reward Optimization (arXiv 2511.19253) \[CHECK authors\]**

Link: [arxiv.org/abs/2511.19253](https://arxiv.org/abs/2511.19253)

Summary: Repositions the LLM as an offline "training architect". An LLM shapes both the tasks and the rewards while a standard MARL backbone optimises the policy, and the LLM is not needed at deployment. Reward shaping and curriculum are coupled: as difficulty changes, the LLM revises both the environment description and the reward logic.

For your project: It combines two of your alternatives (reward adaptation and environment adaptation) in one pipeline, which suggests a hybrid condition for G4. The offline-architect idea also matches your setup, since the LLM stays out of the satellite's control loop and only shapes training.

**19. DrEureka: Language Model Guided Sim-To-Real Transfer (Ma et al., RSS 2024)**

Link: [project page (RPL, UT Austin)](https://rpl.cs.utexas.edu/publications/2024/07/15/ma-rss24-dreureka/)

Summary: Extends Eureka by having an LLM design both the reward function and the domain-randomisation distribution, using a reward-aware prior to propose randomisation configurations, with safety considerations built into the reward. It found sim-to-real configurations competitive with human-designed ones and solved novel tasks without iterative manual design. Ablations without domain randomisation performed much worse.

For your project: Directly relevant to your scope, because you separate the true simulator state from the agent's information. DrEureka shows an LLM can jointly choose reward changes and perturbation ranges, which maps onto changing the reward and the sensor-degradation settings together. It also shows that reward changes alone may not be enough.

### Safety, hacking and robustness (from background knowledge, verify before citing)

**20. Defining and Characterizing Reward Hacking (Skalse et al., NeurIPS 2022) \[CHECK\]**

Link (Google Scholar search, I did not open the paper itself): [search](https://scholar.google.com/scholar?q=Defining+and+Characterizing+Reward+Hacking)

Summary: Gives a formal definition of reward hacking, where optimising a proxy reward lowers the true reward, and analyses when a proxy can be hacked.

For your project: LLM-written rewards are proxies, so this gives the theory for your failure analysis. Report cases where an LLM edit improves fuel use but increases near-miss rates.

**21. Robust Deep RL against Adversarial Perturbations on State Observations (Zhang et al., NeurIPS 2020) \[CHECK\]**

Link (Google Scholar search, I did not open the paper itself): [search](https://scholar.google.com/scholar?q=Robust+Deep+Reinforcement+Learning+against+Adversarial+Perturbations+on+State+Observations)

Summary: Formalises state-adversarial MDPs, where the agent's observation is perturbed while the true state is unchanged, and proposes regularisation to make policies robust to bounded observation perturbations.

For your project: Your simulator already separates true state from observed state, which is the same structure. Use this to formalise sensor degradation, and as a non-reward baseline for robustness.

**22. Constrained Policy Optimization (Achiam et al., ICML 2017) and CMDPs (Altman, 1999) \[CHECK\]**

Links (Google Scholar searches, I did not open these papers): [Constrained Policy Optimization](https://scholar.google.com/scholar?q=Constrained+Policy+Optimization+Achiam) | [Constrained Markov Decision Processes (Altman)](https://scholar.google.com/scholar?q=Altman+Constrained+Markov+Decision+Processes)

Summary: CMDPs maximise reward subject to bounded expected costs. CPO gives a trust-region method with approximate guarantees on constraint satisfaction.

For your project: Background for Mu et al.'s formulation, and for deciding which objectives are hard constraints and which are tradeable reward terms.

**23. A Generalized Algorithm for Multi-Objective RL and Policy Adaptation (Yang et al., NeurIPS 2019) \[CHECK\]**

Link (Google Scholar search, I did not open the paper itself): [search](https://scholar.google.com/scholar?q=A+Generalized+Algorithm+for+Multi-Objective+Reinforcement+Learning+and+Policy+Adaptation)

Summary: Learns a single policy conditioned on a preference vector over objectives, which can adapt to new preferences without retraining from scratch.

For your project: A multi-objective counterpart to RCRL, and a useful baseline when a mission change is just a new weighting over collision, fuel and deviation.

### Satellite collision avoidance

**24. Spacecraft Autonomous Decision-Planning for Collision Avoidance (Bourriez et al., 2023) and Collision Avoidance and Return Manoeuvre Optimisation for Low-Thrust Satellites (Paduraru, ICAART 2025) \[CHECK authors\]**

Links: [Bourriez et al. (arXiv 2310.18966)](https://arxiv.org/abs/2310.18966) | [PPO debris-avoidance preprint (arXiv 2608.09628)](https://arxiv.org/abs/2608.09628) | [Paduraru, ICAART 2025 (Google Scholar search)](https://scholar.google.com/scholar?q=Collision+avoidance+and+return+manoeuvre+optimisation+for+low-thrust+satellites+using+reinforcement+learning)

Summary: Bourriez et al. propose a deep RL framework that assumes imperfect monitoring information about debris and learns stochastic avoidance policies. Paduraru addresses avoidance together with returning to the nominal trajectory for low-thrust satellites. A 2026 arXiv paper on PPO trajectory optimisation for debris avoidance (arXiv 2608.09628) also appears relevant \[CHECK\].

For your project: These add collision-avoidance baselines beyond Mu et al. and cover uncertainty in debris state and trajectory deviation, two of your three objectives.

## Part C. Mapping to your goals

- **G1 (agent under changing conditions):** 5, 14, 15, 6, 7, 21, 24
- **G2 (reward changes):** 13, 1, 12, 20, 22, 23
- **G3 (LLM translation):** 11, 16, 4, 2, 17
- **G4 (iterative loop vs alternatives):** 4, 3, 10, 12, 8, 7, 18, 19, 23

**Gaps still open:** I found no paper that adapts the reward of an already-trained collision-avoidance agent after conditions change, which supports your project's novelty. Searching beyond what I did here (for example Google Scholar for LLM plus spacecraft plus reward) is worth doing before you claim that.
