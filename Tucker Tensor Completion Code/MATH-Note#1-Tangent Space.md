# Derivation of Tangent Space

The tangent space of a Tucker format tensor is given by the paper
**"DYNAMICAL TENSOR APPROXIMATION"** by OTHMAR KOCH, and CHRISTIAN LUBICH


(NEED TO BE REFINED)
 

The derivation of this tangent space looks similar to the tangent space of Stiefel Manifolds 
    (I × r matrices with orthonormal columns)
    The folloing link proves the form of tangent space for Stiefel Manifolds by using diff geo
        https://math.stackexchange.com/questions/477057/on-tangent-spaces-of-stiefel-manifolds


### Tangent Space in Differential Geometry
- **Definition:** The tangent space at a point on a manifold is the set of all possible tangent vectors, each of which is the derivative at that point of some smooth curve lying on the manifold.
- **Smooth Curves:** A single smooth curve $ Y(t)$ through a point $Y(0)$ gives one tangent vector $\dot{Y}(0)$. However, the tangent space $T_{Y(0)}M$ comprises the derivatives of all possible smooth curves passing through $Y(0)$.

### Deriving the Tangent Space for the Tucker Format
- **Tucker Decomposition:** Any tensor $Y$ in the Tucker format can be expressed as  
  $$
  Y = S \times_1 U_1 \times_2 U_2 \cdots \times_N U_N,
  $$
  where $S$ is the core tensor and each $U_n$ is a factor matrix with orthonormal columns.
- **Introducing a Time Parameter $t$:**  
  - A family of tensors $Y(t) = S(t) \times_1 U_1(t) \times_2 \cdots \times_N U_N(t)$ is considered.
  - The time parameter $t$ is used to parameterize a smooth curve on the manifold of tensors, allowing us to study variations around a fixed tensor $Y(0)=Y$.

- **Differentiation and the Tangent Map:**  
  - By differentiating the Tucker decomposition with respect to $t$ using the product rule, one obtains
    $$
    \dot{Y}(t) = \dot{S}(t) \times_1 U_1(t) \times_2 \cdots \times_N U_N(t) + \sum_{n=1}^N S(t) \times_n \dot{U}_n(t) \times_{k \neq n} U_k(t).
    $$
  - This formula represents how small changes in the core tensor $S$ and the factor matrices $U_n$ produce an infinitesimal change in the tensor $Y$.

- **Gauge Conditions for Uniqueness:**  
  - To ensure that the representation of a tangent vector is unique, orthogonality (or gauge) conditions like $U_n^T \dot{U}_n = 0$ are imposed.
  
- **Mapping to the Tangent Space:**  
  - The map  
    $$
    (\dot{S}, \dot{U}_1, \dots, \dot{U}_N) \mapsto \dot{Y} = \dot{S} \times_1 U_1 \times_2 \cdots \times_N U_N + \sum_{n=1}^N S \times_n \dot{U}_n \times_{k\neq n} U_k,
    $$
    is derived by differentiating the Tucker representation.
  

  We can also show that if the Tensor has different Tucker format, but tangent tensor are still the same even with different representation