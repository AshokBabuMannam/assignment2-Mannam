# assignment2-Mannam
## Paraside is my favourite place to have food.
This restuarent is famous for **Hyderabad biryani**, which is near by **Parde ground**.
*************************************************************************************************
# Directions to the Place
### Rajiv Gandhi International Airport
1.  After coming out of Airport.
    1. Book a cab from OLA/Uber to destination as Paraside.
    2. Reserve a table via Online for dining.
2.  After reaching the destination
    1. Show the reserved table details you booked.
    2. Have your seat and ask for Menu card.
    3. Order the list of items you wish to eat and enjoy the food.
    
# Following are the food items
*  Vegeterian 
    * Paneer Butter Masala
    *  Butter Naan
    * Roti
    * Dal Tadkha
    * Panner Biryani 
*  Non Vegererian 
    * Chicken Dum Biryani
    * Chicken SP Biryani 
    * Mutton Biryani         
    * Prawn Biryani

**[About Me Link ](AboutMe.md)**

***************************************************************************
### Sports Activities

|Sport|Location|Amount|
|---|---|---|
|Kabbadi|INDIA|$200|
|Cricket|INDIA|$400|
|BasketBall|USA|$300|
|Soccerr|USA|$400|

*************************************************************************
### Pithy Quotes

The purpose of our lives is to be happy
>   ~ *Dalai Lama*

You only live once, but if you do it right, once is enough
>  ~ *Mae West*

***

# Code Fencing
> Given a set of points in the plane. the convex hull of the set is the smallest convex polygon that contains all the points of it. Using Graham’s scan algorithm, we can find Convex Hull in O(nLogn) time. following is Graham’s algorithm.

Link to Source <https://www.geeksforgeeks.org/convex-hull-set-2-graham-scan/?ref=gcse>
```

struct pt {
    double x, y;
};

int orientation(pt a, pt b, pt c) {
    double v = a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y);
    if (v < 0) return -1; // clockwise
    if (v > 0) return +1; // counter-clockwise
    return 0;
}

bool cw(pt a, pt b, pt c, bool include_collinear) {
    int o = orientation(a, b, c);
    return o < 0 || (include_collinear && o == 0);
}
bool collinear(pt a, pt b, pt c) { return orientation(a, b, c) == 0; }

void convex_hull(vector<pt>& a, bool include_collinear = false) {
    pt p0 = *min_element(a.begin(), a.end(), [](pt a, pt b) {
        return make_pair(a.y, a.x) < make_pair(b.y, b.x);
    });
    sort(a.begin(), a.end(), [&p0](const pt& a, const pt& b) {
        int o = orientation(p0, a, b);
        if (o == 0)
            return (p0.x-a.x)*(p0.x-a.x) + (p0.y-a.y)*(p0.y-a.y)
                < (p0.x-b.x)*(p0.x-b.x) + (p0.y-b.y)*(p0.y-b.y);
        return o < 0;
    });
    if (include_collinear) {
        int i = (int)a.size()-1;
        while (i >= 0 && collinear(p0, a[i], a.back())) i--;
        reverse(a.begin()+i+1, a.end());
    }

    vector<pt> st;
    for (int i = 0; i < (int)a.size(); i++) {
        while (st.size() > 1 && !cw(st[st.size()-2], st.back(), a[i], include_collinear))
            st.pop_back();
        st.push_back(a[i]);
    }

    a = st;
}
```

 Link to Source code <https://cp-algorithms.com/geometry/convex-hull.html>

 > Given a set of points, the task is to find the convex hull of the given points. The convex hull is the smallest convex polygon that contains all the points.  Monotone chain algorithm constructs the convex hull in O(n * log(n)) time. We have to sort the points first and then calculate the upper and lower hulls in O(n) time.

 Link to Source <https://www.geeksforgeeks.org/convex-hull-monotone-chain-algorithm/?ref=gcse>

 ```
 struct pt {
    double x, y;
};

int orientation(pt a, pt b, pt c) {
    double v = a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y);
    if (v < 0) return -1; // clockwise
    if (v > 0) return +1; // counter-clockwise
    return 0;
}

bool cw(pt a, pt b, pt c, bool include_collinear) {
    int o = orientation(a, b, c);
    return o < 0 || (include_collinear && o == 0);
}
bool ccw(pt a, pt b, pt c, bool include_collinear) {
    int o = orientation(a, b, c);
    return o > 0 || (include_collinear && o == 0);
}

void convex_hull(vector<pt>& a, bool include_collinear = false) {
    if (a.size() == 1)
        return;

    sort(a.begin(), a.end(), [](pt a, pt b) {
        return make_pair(a.x, a.y) < make_pair(b.x, b.y);
    });
    pt p1 = a[0], p2 = a.back();
    vector<pt> up, down;
    up.push_back(p1);
    down.push_back(p1);
    for (int i = 1; i < (int)a.size(); i++) {
        if (i == a.size() - 1 || cw(p1, a[i], p2, include_collinear)) {
            while (up.size() >= 2 && !cw(up[up.size()-2], up[up.size()-1], a[i], include_collinear))
                up.pop_back();
            up.push_back(a[i]);
        }
        if (i == a.size() - 1 || ccw(p1, a[i], p2, include_collinear)) {
            while (down.size() >= 2 && !ccw(down[down.size()-2], down[down.size()-1], a[i], include_collinear))
                down.pop_back();
            down.push_back(a[i]);
        }
    }

    if (include_collinear && up.size() == a.size()) {
        reverse(a.begin(), a.end());
        return;
    }
    a.clear();
    for (int i = 0; i < (int)up.size(); i++)
        a.push_back(up[i]);
    for (int i = down.size() - 2; i > 0; i--)
        a.push_back(down[i]);
}

```

Link to Source code <https://cp-algorithms.com/geometry/convex-hull.html>




