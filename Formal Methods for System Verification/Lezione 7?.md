PC Lan situation 
PC1 - PC2
   |	       |
PC4 - PC3
Token ring
The token passes around the network from one node (PC) to another in a round robin order.
Components of the system
PC1...4
Token 
$\lambda$ rate which data packets are generated,
$\mu$ rate which data packets are sent
$\omega$ rate of movement of the token from one pc to another
Two states:
- State 0 -> No data packets to be transmitted
- State 1 -> There is one data packet to be transmitted 
PC_{i0} = (generate, $\lambda)$. PC_i1
PC_i1 = (transmit, $\mu$). PC_i0
Token_i where i=1...4
Token_i = (transmit, $\mu$). PC (walk_i+1, $\omega$ ).Token_i+1 + (walkon_i+1, $\omega$).Token_i+1
Refining the model:
Transmits are not synchronized
PC_i0 = (generate, $\lambda$). PC_i1 + (walkon_i+1, $\omega$ ). PC_i0 + (walk_i+1, $\mu$).PC_i0
Token_i = (transmit_i, $\mu$).(walk_i+1, $\omega$).Token_i+1

LAN=(PC:_10||PC_20||PC_30||PC_40)|><| on L Token_1
L={Walk_i, walkon_i, transmit_i} where i= 1..4

# Semantics of PEPA
$\tau$ -> (a,$\tau$ ) when we don't know the rate of the activity, will be specified later.
A component that has the $\tau$ is incomplete.