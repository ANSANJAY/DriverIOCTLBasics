
You can use __put_user/__get_user if access_ok is already being called. This will save few cycles.

#define put_user(x, ptr)                                        \
({                                                              \
        void __user *__p = (ptr);                               \
        might_fault();                                          \
        access_ok(__p, sizeof(*ptr)) ?          \
                __put_user((x), ((__typeof__(*(ptr)) __user *)__p)) :   \
                -EFAULT;                                        \
})

#define get_user(x, ptr)                                        \
({                                                              \
        const void __user *__p = (ptr);                         \
        might_fault();                                          \
        access_ok(__p, sizeof(*ptr)) ?          \
                __get_user((x), (__typeof__(*(ptr)) __user *)__p) :\
                ((x) = (__typeof__(*(ptr)))0,-EFAULT);          \
})

