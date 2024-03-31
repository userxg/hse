# Binary search approach
## Int sqrt
```C
int sqrt(int n)
{
    int low = 1, high = n;
    while (low < high - 1)
    {
        int mid = (low + high) / 2;
        if (mid * mid == n)
            return mid;
        else if (mid * mid > n)
            high = mid;
        else
            low = mid;
    }
    return -1;
}
```

## Float Sqrt
```C
float sqrt_(float x) {
    float l = 0, r = x + 1;
    while (fabsf(r - l) > 1e-6) {
        float m = (r + l) / 2;
        if (m * m > x) {
            r = m;
        } else {
            l = m;
        }
    }
    return l;
}
```
