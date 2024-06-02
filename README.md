# PrismForce-Coding-Test

ASDE Algorithm Test

Imagine Abhimanyu in Chakravyuha. There are 11 circles in the Chakravyuha surrounded by different enemies.<br>
Abhimanyu is located in the innermost circle and has to cross all the 11 circles to reach Pandavas army back. <br>
<br>
Given:<br>
  Each circle is guarded by different enemy where enemy is equipped with k1, k2……k11 powers<br>
Abhmanyu start from the innermost circle with p power Abhimanyu has a boon to skip fighting enemy<br>
a times <br>
 Abhmanyu can recharge himself with power b times <br>
 Battling in each circle will result in loss of the same power from Abhimanyu as the enemy. <br>
 If Abhmanyu enter the circle with energy less than the respective enemy, he will lose the battle<br>
  k3 and k7 enemies are endured with power to regenerate themselves once with half of their initial<br>
power and can attack Abhimanyu from behind if he is battling in iteratively next circle <br>
<br>
<br>
 
Write an algorithm to find if Abhimanyu can cross the Chakravyuh and test it with two sets of test cases.<br>

Solution:<br>
<br>
Assumption:<br>
-
I have assumed that even if we skip the enemy of circle 3 or circle 7, then it can only attack with half of its intial energy from behind if he is battling in iteratively next cicle that is in circle 4 or 8.<br>

Code:<br>
-
```
#include <bits/stdc++.h>

using namespace std;

int solve(vector<int> &k , int ind , int p , int a , int b){

    if(ind == 12) return 1;               // If Abhimanyu has crossed all circles return true.
    
    int ans = 0;

    int attack = k[ind];

    if(ind == 4 || ind == 8){            // If he is fighting at 4th or 8th circle then the enemy of 3rd or 7th circle can attack from behid with half of its energy
        attack += (k[ind-1] / 2);
    }

    if(p >= attack) {                    // If power of Abhimanyu is greater than or equal to the power of attack of that circle
        ans |= solve(k , ind+1 , p-attack , a , b);
    }
    else {                              // If If power of Abhimanyu is less than the power of attack of that circle
        int d = attack - p;
        if(b >= d){
            ans |= solve(k , ind+1 , 0 , a , b-d);
        }
    }

    // If the number of skips is still left
    
    if(a > 0) ans |= solve(k , ind+1 , p , a-1 , b);

    return ans;
}

int main(){

    int p , a , b;
    
    cin>>p>>a>>b;                     // Taking input of intial power of Abhimanyu, No of skips, No of times he can recharge

    vector<int> k(12);
    for(int i = 1; i <= 11 ; i ++){
        cin >> k[i];                    // Taking input of power of enemy at each circle
    }

    int ans = solve(k , 1 , p , a , b);           // Calling the function

    cout << ans << endl;                          // Printing the answer.
    return 0;
}
```
Explanation:
-
-I have used simple recursion here, since the number of circle is 11 only.

-At each circle, Abhimanyu has few choices to take.

-If the power of Abhimanyu is greater than or equal to power of enemy, he can fight with it.

-Else if not, he can recharge its power to that of enemy if possible(depends on b).

-Or If there is still a chance of skip, he can take that option (depends on a).

-If Abhimanyu crosses all circles, true is returned else false is returned.
