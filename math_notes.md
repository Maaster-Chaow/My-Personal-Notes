# Math Notes

## Abstract Algebra

* **Center of a group** : The center of a group $G$, denoted as $Z(G)$ is
  defined as:
    $$Z(G) := \{ g \in G\,|\,a\,g = g\,a \textrm{ for every } a \in G \}.$$

* **Centralizer of an Element** : The centralizer of an element $a$ of a
  group $G$, denoted by $C(a)$ is given as:
    $$C(a) := \{ g \in G\,\,|\,\,g\,a = a\,g \}.$$

* **Homomorphism of groups** : Let $G$ and $G'$ be two groups.
  A _homomorphism of groups_ is a function
    $$\Phi : G \rightarrow G'.$$
  such that,
    $$\Phi(ab) = \Phi(a)\,\Phi(b) \textrm{ for all } a, b \in G.$$

* **Properties of group homomorphism** : Let $\Phi : G \rightarrow G'$ be a
  group homomorphism. Then
  1. $\Phi(e_{G}) = e_{G'}$.
  2. If $a \in G$, then $\Phi(a^{-1}) = (\Phi(a))^{-1}$.

* **Kernel of homomorphism of a group** : Let $\Phi : G \rightarrow G'$ be
  a group homomorphism. Then the _kernel of $\Phi$_ $Ker(\Phi)$ is given as:
    $$ Ker(\Phi) = \{ a \in G\,\,|\,\,\Phi(a) = e_{G'} \}.$$

* **Image of a homomorphism of a group** : Let $\Phi : G \rightarrow G'$ be a
  group homomorphism. Then the _image of $\Phi$_ $Img(\Phi)$ is given as:
    $$Img(\Phi) = \{ \Phi(a)\,\,|\,\,a \in G \}.$$
