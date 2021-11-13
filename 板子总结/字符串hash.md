//字符串hash

~~~fake 
// p = 131 或133
f[i] = s[i] - 'a' + f[i - 1]*p 表示0到i字符串的hash值

f[j] - f[i ] * p^j 表示字符串s[i]到s[j]的hash值

~~~

#

(a/b) % mod == a * b1 % mod

b1 = b^(mod - 2)