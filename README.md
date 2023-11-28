[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=13027387&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions



Let's break down the recursive procedure to analyze its runtime. To start, the function has three nested loops. The outer loop runs n^2 times, the middle loop runs n times, and the inner loop runs n^2 times. Thus, there will be  $\n^5$ iterations. Now, let's formulate the recursive relation. Let T(n) represent the time complexity of the function for a given input size n. The recurrence relation for the runtime of the mystery function is $T(n)=3T(n/3)+O(n^5)$. This relation comes from the three recursive calls with the parameter n / 3 and the complexity within the loops being O(n^5). To solve this recurrence relation, we can apply the Master Theorem. In this case, a=3, b=3, and f(n)=O(n^5).
The Master theorem states:
    1. If f(n) = O($n^c$) where $c<log⁡_b(a)$, then $T(n)=Θ(log⁡b(a))$.
    2. If f(n) = Θ($n^clog⁡k(n)$) where $c=log⁡b(a)$, then $T(n)=Θ(n^clog⁡^(k+1)(n))$.
    3. If f(n) = Ω($n^c$) where c>log⁡b(a), and af(n/b)≤kf(n) for some k<1 and sufficiently large n, then         $T(n)=Θ(f(n))$.
Comparing f(n)=O($n^5$) with $log⁡3(3)$, we have c=5 and $log⁡_3(3)$=1.
Here, c>log⁡b(a)c>logb(a), so the third case of the Master theorem applies. Therefore, the tight bound for the runtime of the function is Θ($n^5$).

We can test this without using Masters Theorem. So, we know the recurrence relation for the runtime of the mystery function is $T(n)=3T(n/3)+O(n^5)$. If we plug it into itself, we can see a trend and create an expression representing the runtime. The first time we get $9T(n/3/3)+3n^5/n^5+n^5$. Then we have $9(3T(n/9/3+n^5/9)^5+n^{12}/27+n^5$ which simplifies down to $27T(n/27)+n^{5}/3^9+n^5/3^3+n^5$. Notice the trend with similar values that change at the same time. With this in mind, we come up with:
$$3^iT(n/3^i)+\left( \sum_{j=0}^{i-1}n^5/3^{3j} \right)$$ How often can we divide a number by 3 until we reach the base case? We can represent it as $log_3n$ which we can substitute for i. $3^{log_3n}=n$ so n+1 for the i expression. J is just a constant, but the i is replaced with $logn-1$, so were left with $n*1+n^5$. Thus, the tight big O bound is $Θ(n+n^5)$ or just $Θ(n^5)$ when we remove the constant. 

Nicholas Matter, Assignment 1, 20 Sep 2022

