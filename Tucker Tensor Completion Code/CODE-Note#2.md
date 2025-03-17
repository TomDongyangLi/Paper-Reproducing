### Differences between My code and the Matlab code
#### 1. Data Generation
|Data Generation| My Code | Matlab Code |
|------------|----------|------------|
|     Core tensor   $\mathcal{C}$    |      both uniformly                 |
|   matrix factor  $U_i$       |    both uniformly and then QR decomposition | $Q$ is the new $U_i$, $R$ is combined with $C$      
|full tensor|   calculated |  not calculated |
|Storage|   Tucker format & full tensor |    Tucker format   |

##### Improvement: 
1. use `torch.tensordot` combining $R$ to $\mathcal{C}$ instead of unfolding, then multiplication, then folding back

2.  maybe don't store the full tensor, even though we only generate data once for each setting, try to avoid using full tensor during the algorithm, 



#### 2. Sampling strategy
|Sampling |My Code| Matlab Code|
|---------|-------|------------|
|distribution   |both uniformly |          |
|# of sampling   |    less      |    exact    (unique) |
|Index|tensor |tensor|
|storage of sampling |full tensor|sparse tensor|


##### Improvement:
1. use exact number of sampling

2. Use $\mathcal{A}_{\Omega} = P_\Omega(\mathcal{A})$ instead of $P_\Omega(\mathcal{A})$. 

3. Store $A_\Omega$ as sparse tensor 

4. easier way to calculate norm with sparse tensor?

#### 3. Riemannian Gradient and linear search
Matlab uses this mex file that can't be open, so we cannot find the difference. But, we do find out that 

- Euclidean gradient is in sparse tensor
- Riemannian gradient $\xi$ is in Tangent space  format
- conjugate direction $\eta$ is in Tangent space format

Difference: 
- MATLAB only calculate the factors in tangent format
- My Code not only calculate the factors but also calculates the full tensor in the tangent space 


#### 4. Retraction
- **MATLAB CODE**: Utilize Tanget format and Tucker format. Details in section 3.3 of paper. Find the combined tensor $\mathcal{S}$. Do orthgonalization, update $\mathcal{S}$, Do HOSVD for $\mathcal{S}$, which has much smaller size then full tensor. After retraction, the tensor is stored in Tucker format. 

- **MY CODE**: Add full tensor, do HOSVD for full tensor. 


## Summary:
- exact number of sampling
- norm of sparse tensor
-  utilize the sparsity, the Tucker format, and the Tangent tensor format. 
    - $\mathcal{A}_\Omega$, Euclidean Gradient $\mathcal{E}$ as Sparse Tensor
    - $\mathcal{A},\mathcal{X}_k$ as Tucker format
    - $\xi$, the Riemanian gradient, and $\eta$, the conjugate direction, as Tanget format 

- The Tucker format is useful calculating Riemannian gradient on tangent space. 

- Avoid using full tensor as much as possible. If calculating full tensor, that's fine, but HOSVD needs to be implemented everytime we need Tucker format, which is time consuming. 

- HOSVD is used for $\mathcal{S}$, the combined tensor, but since it's really small, not that time consuming. 

- replace  `reshape` method with `tensordot`, will give much cleaner code. 

- check the details in section 3.2 & 3.3

### Challenges:
- how to get the $\mathcal{A}_\Omega$ sparse tensor from Tucker format of $\mathcal{A}$ using $\Omega$
- how to perform `tensordot` for sparse tensor $\mathcal{E}$. (`ttm` in TT-Toolbox)