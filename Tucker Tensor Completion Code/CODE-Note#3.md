# Changes made to Improve the code

## Data Generator:
- use `tensordot` instead of kronecker product
- kron took much more time than tensordot

## Data Sampling: 
- use `torch.unique` to sample exact number of elements uniformly and with replacement
- sample flat indices first then transform to multi-dim indices

## Sampling Data: 
- didn't change anything, still using whole tensor to access the sampled elements

## Projection over Tangent space
- use `tensordot` instead of kronecker product
- ***DO WE NEED TO FIND THE FULL TENSOR ON TANGENT SPACE?***

## Retraction
- not simply SVD, but utilize the structure of Tangent format (Sec. 3.3)
- ***DO WE NEED TO RETURN THE NEXT STATE AS FULL TENSOR?***



## NOTES:
IMPROVEMENTS WORKED, less running time for each iterations

BUT STILL not comparable to the results in paper when tensor size is over 300

**BUT, WE HAVE MY CODE RUNNING TIME SIMILAR TO MATLAB CODE NOW ON MY MAC**

**WE CAN STOP FOR NOW**

TIME COMPUTATIONAL PART INCLUDES (n = 300, r= 10):
- Riemanian Grad $\sim 0.3$ sec/iter
    - PTxM
- $\beta_k$ in conjugate updation $\sim 0.3$ sec/iter
- Conjugate gradient $\sim 0.3$ sec/iter
- backtracking $\sim 0.2$ sec/iter
- error $\sim 0.2$ sec/iter


## Further Improvements
- backtracking can be omitted, does not affect the performance
- **MUST** lower down the ***error*** computation time.
- PTxM
    - V_core
    - V_proj
- Full tensor?
