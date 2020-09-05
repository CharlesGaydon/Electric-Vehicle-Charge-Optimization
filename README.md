# Electric-Vehicle-Charge-Optimization
Simple EV charge optimization implementation based on `Hoke (2011): Electric Vehicle Charge Optimization Including Effects of Lithium-Ion Battery Degradation` (accessible in `doc`).

## Notebooks

Models are in `src\notebooks`

Model 1:
- An electric vehicle (EV) can charge within a time window (t_min;t_max), from a charge infrastructure with varying electricity prices.

Model 2:
- Both V2G and G2V charges are allowed: the EV acts as a battery that helps balance offer and demand.
- However, charging degrades the battery, and this is accounted by an Arrhenius relationship inspired from Hoke 2011, here with arbitrary parameters.

Model 3:
- Furthermore, battery degradation associated attributable to SOC is accounted for. Minimal SOC of 0.2 is set to be consistent with Hoke 2011 mention of manufacturer-specified battery vehicle protection controls. 

Key observations:
- V2G charge occurs at higher electricity prices, while G2V occurs at lower prices. This behavior has economic interests for the consumer, and would help balance the grid demand and offer if the electricity prices translate (as they should).
- The higher degradation encountered at higher power charges is captured here (although with arbitrary parameters): as higher charges are associated with increase in temperature and thus increased battery degradation, charge profile occur at a constant power on periods of constant electricity prices (e.g. two consecutive 3kWh charges are preferred to one 6kWh charge and one null charge). Without this effect, for instance with a degradation linear to the power charge, charge powers are herratic (not shown here). 
- Coherent with Hoke 2011, charging is delayed to prevent long period with high SOC. A balance is found between reducing high charge power while also reducing amount of time spent with high SOC.


## Python setup
Runs on python 3.7, using scipy's optimization tools, on a virtual environment created via:

	mkvirtualenv evco_env -r requirements.txt

and used via:

	workon evco_env