## Implementing Business Logic

While boilerplate is the low-hanging fruit, modern AI models are increasingly capable of implementing complex, core business logic based on a well-written spec. This is where the quality of your specification pays the greatest dividends.

Let's imagine we're building an e-commerce application. Our spec file, `checkout.spec.md`, might contain the following section:

````markdown
# Feature: Coupon Code Application

## Logic:

1.  The system accepts a shopping cart object and a coupon code string.
2.  It must validate the coupon code against a list of valid codes.
3.  Valid coupon codes have different types:
    - `PERCENT`: Reduces the total cart value by a percentage (e.g., 10% off).
    - `FIXED`: Reduces the total cart value by a fixed amount (e.g., $5 off).
    - `FREE_SHIPPING`: Sets the shipping cost to zero, but only if the cart subtotal is over $50.
4.  The function should return a new cart object with the discount applied and the final total calculated.
5.  If the coupon code is invalid or expired, an error should be thrown.
6.  A coupon cannot reduce the cart total below zero. The minimum total is $0.
````

**Prompt to the AI Agent:**

> "In the `src/logic/checkout.ts` file, implement the coupon code logic defined in `checkout.spec.md`. Assume the existence of a `getCouponByCode(code)` function that returns a coupon object or `null`. Define the necessary TypeScript types for the `Cart` and `Coupon` objects."

The AI would then generate the TypeScript code, including the type definitions and the core function:

```typescript
// AI-Generated Code

interface Cart {
    items: { id: string; price: number; quantity: number }[];
    subtotal: number;
    shippingCost: number;
    discount: number;
    total: number;
}

type CouponType = 'PERCENT' | 'FIXED' | 'FREE_SHIPPING';

interface Coupon {
    code: string;
    type: CouponType;
    value: number; // Percentage for 'PERCENT', amount for 'FIXED'
    isExpired: boolean;
}

// Assume this function is defined elsewhere
declare function getCouponByCode(code: string): Promise<Coupon | null>;

export async function applyCoupon(cart: Cart, code: string): Promise<Cart> {
    const coupon = await getCouponByCode(code);

    if (!coupon || coupon.isExpired) {
        throw new Error("Invalid or expired coupon code.");
    }

    let newCart = { ...cart };
    let discountAmount = 0;

    switch (coupon.type) {
        case 'PERCENT':
            discountAmount = newCart.subtotal * (coupon.value / 100);
            break;
        case 'FIXED':
            discountAmount = coupon.value;
            break;
        case 'FREE_SHIPPING':
            if (newCart.subtotal > 50) {
                newCart.shippingCost = 0;
            }
            break;
    }

    // Ensure total doesn't go below zero
    newCart.discount = Math.min(discountAmount, newCart.subtotal);
    newCart.total = newCart.subtotal - newCart.discount + newCart.shippingCost;
    if (newCart.total < 0) {
        newCart.total = 0;
    }

    return newCart;
}
```

The developer's job is now to read this generated code and ask critical questions: Does it correctly handle the `FREE_SHIPPING` subtotal condition? Does it prevent the total from becoming negative? Is the logic clear and maintainable? The cognitive load shifts from *writing* the logic to *auditing* it—a faster and less error-prone activity.