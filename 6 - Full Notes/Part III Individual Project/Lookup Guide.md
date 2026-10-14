# Quick-Lookup Guide: Which Paper Solves Which Problem

Oct 14, 2026 · @sam

Find your problem in section 1, the symptom in section 3, or the project stage in section 4; each row names the paper (P1-P24, same numbering as the Annotated Paper Summaries doc) and exactly what to take from it.

## 1. I need to... (problem to paper)

| Problem                                                              | Go to                                    | Take from it                                                                                                            |
| -------------------------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Choose state, action and reward for the collision-avoidance agent    | P5 Mu et al. 2024                        | LSTM encoding for a variable number of debris; CMDP solved with P3O. Read the full text for their reward and cost terms |
| Handle uncertain or imperfect debris information                     | P24 Bourriez et al. 2023                 | Stochastic policies trained with imperfect debris monitoring                                                            |
| Include return to the nominal trajectory (deviation objective)       | P24 Paduraru 2025                        | Avoidance plus return manoeuvre for low-thrust satellites                                                               |
| Pick realistic metrics and risk thresholds                           | P14 NASA CARA                            | Probability of collision (Pc), miss distance, covariance; check the site for current thresholds                         |
| Decide what is a hard constraint and what is a tradeable reward term | P22 CMDP/CPO, P5                         | Safety as a constraint; let the LLM edit only soft terms                                                                |
| Model sensor failure or degraded observations                        | P21 Zhang et al. 2020                    | True state unchanged, observation perturbed; robustness baseline                                                        |
| Make degradations graded instead of one-off                          | P7 ACCEL                                 | Small edits to an existing scenario (add debris, shift miss distance, cut thrust 10%)                                   |
| Stop stress tests being impossible                                   | P6 PAIRED, P9 Eurekaverse                | Regret and learnability; reject scenarios with no safe action                                                           |
| Measure how fast an agent adapts                                     | P15 Narvekar et al. 2020                 | Time to threshold, jumpstart, asymptotic performance                                                                    |
| Tell whether a reward edit changes the optimal policy                | P13 Ng et al. 1999                       | Potential-based F = γΦ(s') − Φ(s) preserves the optimum; other edits can change it                                      |
| Explain a reward that scores well but behaves badly                  | P20 Skalse et al. 2022                   | Reward hacking: optimising a proxy lowers the true objective                                                            |
| Name and position my method                                          | P1 Baybas et al. 2026, P17 survey        | Mine is external-feedback-driven; a priority-conditioned reward is context-driven                                       |
| Handle changing priorities without retraining                        | P12 RCRL, P23 Yang et al. 2019           | Condition the policy on objective weights; zero-shot adjustment                                                         |
| Turn a mission statement into reward code                            | P11 Text2Reward, P16 Language to Rewards | Give the LLM a structured environment abstraction; reward code as the interface                                         |
| Run the generate, train, reflect loop                                | P4 Eureka                                | Several candidates per iteration; per-component logging as feedback                                                     |
| Keep collision, fuel and deviation balanced                          | P2 Balancing Act                         | LLM proposes, a fixed rule selects                                                                                      |
| Cut the number of training runs                                      | P10 CARD                                 | Pre-screen candidates with trajectory-preference checks                                                                 |
| Know what results to expect from a satellite LLM-reward pipeline     | P3 LARGE                                 | Gains within a few iterations, near expert quality, mixed across metrics                                                |
| Change reward and sensor-degradation settings together               | P19 DrEureka                             | LLM designs reward and randomisation ranges jointly                                                                     |
| Have the LLM adapt the training environment                          | P8 EnvGen, P18 MAESTRO                   | Environment configs from weakness reports; offline LLM shapes tasks and rewards                                         |

## 2. Comparison conditions for goal 4

| Condition | What it is | Paper | Question it answers |
| --- | --- | --- | --- |
| No adaptation | Original agent under the new condition | P5 | How bad is the degradation? |
| Manual reward edit | Hand-written reward change (expert baseline) | P3, P4 | Can the LLM match an expert? |
| One-shot LLM | LLM writes the reward once, no feedback | P11, P16 | Does feedback add value? |
| Iterative LLM | Generate, train, reflect, revise | P4, P3 | The main method |
| Reward-conditioned policy | Policy takes objective weights as input | P12, P23 | Is retraining or an LLM needed at all? |
| Environment adaptation | Change training scenarios, not the reward | P8, P7, P6 | Reward change vs scenario change |
| Hybrid | LLM edits reward and scenarios | P18, P19 | Do they combine well? |
| Fine-tune vs retrain | Continue training vs start again | P15 | Cost to adapt |

## 3. Something is going wrong (symptom to fix)

| Symptom | Likely cause | Try | Paper |
| --- | --- | --- | --- |
| Fuel use improves but collisions rise | LLM trades safety for the objective it was asked to improve | Score candidates on collision first with a fixed selection rule; keep safety as a constraint | P2, P5, P20 |
| Reward gets worse over iterations | Noisy feedback, one candidate per iteration | Sample several candidates and keep the best so far | P4, P3 |
| LLM ignores or overuses one reward term | It only sees total return | Log each component's contribution and feed it back | P4 |
| Too many training runs | Every candidate trained fully | Pre-screen with a preference check on safe vs collision trajectories | P10 |
| Generated reward code crashes | LLM guessing the simulator's interface | Provide a structured abstraction; retry on execution errors | P11 |
| Agent fails in a degraded scenario and nothing helps | Scenario may be infeasible | Add a feasibility check before using it | P6, P9 |
| Reward edit changes learning speed but not behaviour | It is pure shaping | Classify with the potential-based test | P13 |
| Policy cannot follow new priority weights | Weights outside the trained family | Conditioned policies cover only trained reward families; use the LLM for genuinely new terms | P12 |
| Gains do not transfer to other degradations | Overfit to one scenario | Evaluate on a graded set; vary degradation settings in training | P7, P19, P21 |
| Mixed results across metrics | Normal in this setting | Report all metrics against the expert baseline | P3 |
| Learning destabilises when the reward changes | Large or frequent changes (my suggestion, no paper) | Limit how much and how often the reward changes between runs | none |

## 4. Method path (stage to paper)

1. Define the agent, state, action and constraints: P5, P22.
2. Fix evaluation metrics: P14, P15.
3. Train the nominal agent and measure degradation across graded conditions: P7, P21, P6.
4. Give the LLM the mission change and a structured environment abstraction: P11, P16.
5. Generate several candidate rewards with per-component logging: P4.
6. Pre-screen candidates and classify the edits: P10, P13.
7. Train, evaluate and select with a fixed rule: P2.
8. Feed component statistics back and iterate: P4, P3.
9. Compare against the conditions in section 2.
10. Report every metric and the failure cases: P3, P20.

## 5. Paper cheat sheet

| P | Paper | Core idea | Link |
| --- | --- | --- | --- |
| 1 | Adaptive Reward Design survey (2026) | Taxonomy by driver of reward change | [IJCAI](https://www.ijcai.org/proceedings/2026/863) |
| 2 | Balancing Act (2024) | LLM generates, social-choice rule selects | [arXiv](https://arxiv.org/abs/2408.12112) |
| 3 | LARGE, LEO routing (2026) | LLM reward plus simulator feedback near expert level | [arXiv](https://arxiv.org/abs/2608.01649) |
| 4 | Eureka (2024) | Evolutionary LLM reward search with reward reflection | [arXiv](https://arxiv.org/abs/2310.12931) |
| 5 | Mu et al. (2024) | Safe RL, variable debris count, LSTM, P3O | [DOI](https://doi.org/10.1016/j.ast.2024.109131) |
| 6 | PAIRED (2020) | Regret-based adversarial environment design | [arXiv](https://arxiv.org/abs/2012.02096) |
| 7 | ACCEL (2022) | Small edits to high-regret levels | [PMLR](https://proceedings.mlr.press/v162/parker-holder22a.html) |
| 8 | EnvGen (2024) | LLM environments from agent weakness reports | [arXiv](https://arxiv.org/abs/2403.12014) |
| 9 | Eurekaverse (2025) | LLM-generated learnable curriculum | [PMLR](https://proceedings.mlr.press/v270/liang25a.html) |
| 10 | CARD (2024) | Trajectory-preference pre-screening | [arXiv](https://arxiv.org/abs/2410.14660) |
| 11 | Text2Reward (2024) | Language goal to dense reward code | [arXiv](https://arxiv.org/abs/2309.11489) |
| 12 | Reward-Conditioned RL (2026) | Policy conditioned on reward parameters | [arXiv](https://arxiv.org/abs/2603.05066) |
| 13 | Ng et al. (1999) | Potential-based shaping preserves the optimal policy | [PDF](https://ai.stanford.edu/~ang/papers/shaping-icml99.pdf) |
| 14 | NASA CARA | Pc, miss distance, thresholds | [NASA](https://www.nasa.gov/cara/) |
| 15 | Narvekar et al. (2020) | Curriculum framework and evaluation metrics | [JMLR](https://jmlr.org/beta/papers/v21/20-212.html) |
| 16 | Language to Rewards (2023) | Reward as the language-to-control interface | [arXiv](https://arxiv.org/abs/2306.08647) |
| 17 | LLM/VLM-integrated RL survey | Where LLMs sit in RL; reward-design section | [arXiv](https://arxiv.org/abs/2502.15214) |
| 18 | MAESTRO | Offline LLM shapes tasks and rewards | [arXiv](https://arxiv.org/abs/2511.19253) |
| 19 | DrEureka (2024) | LLM designs reward and domain randomisation | [Project](https://rpl.cs.utexas.edu/publications/2024/07/15/ma-rss24-dreureka/) |
| 20 | Skalse et al. (2022) | Formal reward hacking | [Scholar](https://scholar.google.com/scholar?q=Defining+and+Characterizing+Reward+Hacking) |
| 21 | Zhang et al. (2020) | State-adversarial MDPs, observation robustness | [Scholar](https://scholar.google.com/scholar?q=Robust+Deep+Reinforcement+Learning+against+Adversarial+Perturbations+on+State+Observations) |
| 22 | CPO and CMDPs | Constrained RL background | [Scholar](https://scholar.google.com/scholar?q=Constrained+Policy+Optimization+Achiam) |
| 23 | Yang et al. (2019) | Preference-conditioned multi-objective RL | [Scholar](https://scholar.google.com/scholar?q=A+Generalized+Algorithm+for+Multi-Objective+Reinforcement+Learning+and+Policy+Adaptation) |
| 24 | Bourriez (2023), Paduraru (2025), PPO preprint | More collision-avoidance baselines | [Bourriez](https://arxiv.org/abs/2310.18966) |

## 6. Confidence notes

Rows built on P20 to P23 and the P24 Paduraru paper rely on my background knowledge and Scholar-search links, so confirm them in the full text before citing. For P5 I read only the abstract, so check the reward and cost terms yourself before relying on that row. The few rows that cite no paper are my own suggestions.
