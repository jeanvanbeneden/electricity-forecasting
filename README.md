# Belgian Electricity Price Forecasting



This project implements a Temporal Fusion Transformer to forecast day-ahead electricity prices on the Belgian market (ENTSO-E transparency platform data). 

The initial goal was to benchmark state-of-the-art Deep Learning models on price forecasting. However, the analysis revealed significant limitations of pure time-series approaches.

## Key Results

After optimizing hyperparameters with Optuna and restricting training to the pre-crisis homogeneous period (2018-2021), the model achieved a Mean Absolute Error (MAE) of 7.91 EUR/MWh on the test set.
While this performance is solid for "normal" regimes, an error breakdown reveals a systematic failure mode:

- Normal hours: MAE ~ 5.7 EUR/MWh (Excellent accuracy).
- Price spikes: Errors increase by a factor of 26.


## Failure Analysis

The model systematically underperforms during specific windows:
1. Evening peaks (18h-20h): When supply margins are tight.
2. Weekends: High renewable penetration + lower demand.




## Conclusion :

The correlation between high errors and scarcity events suggests that price formation during these periods is driven by strategic bidding behavior (generators maximizing profit under constraints) rather than historical statistical patterns.

This limitation confirms for me that pure Deep Learning models are insufficient for regime-switching markets. Accurate forecasting of extreme events likely requires hybrid approaches incorporating the startegy of the actors. This could be done using Game Theory or Control Theory. In fact, optimization under constraints is precisely what Control Theory addresses, while strategic interactions between actors is pure Game Theory!

## Future Improvements:

*Model Comparison*:
- Test N-BEATS, LSTM, GRU to verify failure patterns are architecture-independent
- Explore physics-informed neural networks incorporating grid constraints

*Analysis Extensions*:
- Multi-horizon forecasting (J+2, J+3) to quantify degradation rate
- Transfer learning across European markets

*Strategic Behavior Validation*:
- Build simple agent-based market simulation with strategic bidding rules
- Compare ML performance on "honest bidding" vs "strategic bidding" scenarios

*Theoretical Extensions*:
- Model producers as game-theoretic agents 
- Formulate as distributed optimization problem 
- Connection to control theory : each producer as a controller with constraints

The failure of the model points toward game theory and control theory, but actually implementing those approaches is a different (and harder) project.

