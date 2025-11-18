
# 1. TypeScript: `interface` এবং `type` এর মধ্যে পার্থক্য

TypeScript-এ `interface` এবং `type` দুটিই type definition তৈরির জন্য ব্যবহার করা হয়, তবে তাদের মধ্যে কিছু গুরুত্বপূর্ণ পার্থক্য রয়েছে।

##  মূল পার্থক্যসমূহ

### ১. `type` বেশি শক্তিশালী 

`type` দিয়ে primitive types, union types, tuple, এবং advanced types সব তৈরি করা যায়।
```typescript
type ID = string | number;
type Point = [number, number];
type Status = "active" | "inactive" | "pending";
```

### ২. `interface` শুধুমাত্র object structure তৈরির জন্য

`interface` মূলত object-এর structure বা shape define করতে ব্যবহৃত হয়।
```typescript
interface User {
  name: string;
  age: number;
}
```

### ৩. Declaration Merging: `interface` merge হয়, `type` হয় না

একই নামে একাধিক `interface` ঘোষণা করলে সেগুলো স্বয়ংক্রিয়ভাবে merge হয়ে যায়।
```typescript
interface User {
  name: string;
}

interface User {
  age: number;
}
```

কিন্তু `type` এর ক্ষেত্রে একই নামে দুবার ঘোষণা করলে **error** হবে।
```typescript
type User = { name: string };
type User = { age: number }; 
```

### ৪. Class Implementation: `interface` বেশি উপযুক্ত

Class-এ `implements` keyword ব্যবহার করে contract তৈরির জন্য `interface` বেশি জনপ্রিয় এবং উপযুক্ত।
```typescript
interface Animal {
  name: string;
  makeSound(): void;
}

class Dog implements Animal {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  makeSound(): void {
    console.log("Woof!");
  }
}
```

##  কখন কোনটি ব্যবহার করবেন?

| পরিস্থিতি | ব্যবহার করুন |
|---------|--------------|
| Object shape define করতে | `interface` |
| Union/Intersection types তৈরি করতে | `type` |
| Class contract তৈরি করতে | `interface` |
| Primitive/Tuple types তৈরি করতে | `type` |
| Declaration merging প্রয়োজন | `interface` |

##  সারসংক্ষেপ

- **`type`** = বহুমুখী এবং শক্তিশালী, সব ধরনের type definition এর জন্য
- **`interface`** = Object-oriented design এবং class-based architecture এর জন্য আদর্শ

---

# 2. What is the use of the keyof keyword in TypeScript? Provide an example.?

TypeScript-এ keyof অপারেটর একটি অবজেক্ট টাইপের সমস্ত কী থেকে একটি স্ট্রিং বা সাংখ্যিক ইউনিয়ন টাইপ তৈরি করে। সহজভাবে বলতে গেলে, এটি অবজেক্টের প্রপার্টির নামকে একটি নির্দিষ্ট টাইপে রূপান্তরিত করে। এর ফলে কোড আরও নিরাপদ হয় এবং টাইপ-চেকিং সহজ হয়ে যায়.

keyof ব্যবহার করে আমরা একটি interface বা type থেকে শুধুমাত্র কী-গুলো বের করতে পারি এবং একটি নতুন টাইপ তৈরি করতে পারি। এটি বিশেষভাবে জেনেরিক ফাংশনে উপকারী, কারণ এটি ফাংশনের প্যারামিটারকে অবজেক্টের বিদ্যমান কী-এর মধ্যে সীমাবদ্ধ রাখে
keyof ব্যবহারের সুবিধা

টাইপ সেফটি:
ফাংশনে অবজেক্টের কী পাস করার সময় TypeScript নিশ্চিত করে যে আপনি শুধুমাত্র বিদ্যমান প্রপার্টি ব্যবহার করছেন।

জেনেরিক ফাংশন তৈরি করে এটি বিভিন্ন অবজেক্ট টাইপের সাথে কাজ করতে পারে।

যদি অবজেক্টের প্রপার্টির নাম পরিবর্তন হয়, keyof স্বয়ংক্রিয়ভাবে নতুন টাইপ তৈরি করে, ফলে কোড আপডেট করা সহজ হয়।
nterface Person {
  name: string;
  age: number;
}
keyof Person:

"name" | "age"
