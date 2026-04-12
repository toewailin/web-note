ဟုတ်တယ်ဗျ၊ အဲ့ဒါကို **Hydration Error** ဒါမှမဟုတ် **Hydration Mismatch** လို့ ခေါ်ပါတယ်။ Next.js (သို့မဟုတ် React SSR) မှာ အဖြစ်အများဆုံးနဲ့ အနှောင့်အယှက်ပေးဆုံး ပြဿနာတစ်ခုပေါ့။

ဆရာတစ်ယောက်အနေနဲ့ ဒီပြဿနာ ဘာကြောင့်ဖြစ်ရသလဲနဲ့ ဘယ်လိုဖြေရှင်းရမလဲဆိုတာ သေချာရှင်းပြပေးပါမယ်။

---

## ၁။ ဘာကြောင့် ဖြစ်ရတာလဲ? (The Concept)

Next.js ရဲ့ SSR (Server-Side Rendering) အလုပ်လုပ်ပုံက အဆင့် ၂ ဆင့် ရှိပါတယ်။

1.  **Server ပေါ်မှာ:** Next.js က React Code ကို HTML အဖြစ် ပြောင်းလိုက်တယ်။ ပြီးရင် Browser ဆီ ပို့ပေးလိုက်တယ်။ (ဒါက မြန်မြန်ဆန်ဆန် ပေါ်လာအောင်လို့ပါ)။
2.  **Client (Browser) ပေါ်မှာ:** Browser က ရလာတဲ့ HTML ကို ပြတယ်၊ ပြီးရင် React က အဲ့ဒီ HTML ပေါ်မှာ Event Listener တွေ (Click နှိပ်တာတွေ) ပြန်လိုက်တပ်တယ်။ ဒါကို **Hydration** လို့ ခေါ်ပါတယ်။

**ပြဿနာက ဘယ်မှာတက်တာလဲ?**
Server က ထုတ်ပေးလိုက်တဲ့ HTML နဲ့ Client မှာ React က ပထမဆုံး Render လုပ်လိုက်တဲ့ Result မတူတဲ့အခါ React က "ဟေ့... မတူဘူး ဖြစ်နေတယ်" ဆိုပြီး Error တက်တာပါ။



---

## ၂။ ဘယ်လို အခြေအနေမျိုးမှာ အဖြစ်များလဲ?

### က။ Browser-only APIs သုံးမိတဲ့အခါ
Server မှာ `window` တို့ `localStorage` တို့ မရှိပါဘူး။ 
```javascript
// Server မှာ window.innerWidth က မရှိတော့ ပတ်ချာလည်ပြေးနေမယ်
// Client ရောက်မှ window.innerWidth က တန်ဖိုးတစ်ခု ထွက်လာမယ်
const width = typeof window !== 'undefined' ? window.innerWidth : 0;
```
ဒီမှာတင် Server က ထုတ်တဲ့ HTML နဲ့ Client က HTML ကွဲသွားပါပြီ။

### ခ။ အချိန်နဲ့ ရက်စွဲ (Date & Time)
```javascript
<p>{new Date().toLocaleTimeString()}</p>
```
Server က Render လုပ်တဲ့အချိန် (ဥပမာ 10:00:00) နဲ့ Client ဆီ HTML ရောက်ပြီး React ပြန်ပတ်တဲ့အချိန် (ဥပမာ 10:00:01) တစ်စက္ကန့်လောက် ကွာသွားရင်တောင် Error တက်ပါတယ်။

---

## ၃။ ဘယ်လို ဖြေရှင်းမလဲ? (Solutions)

ဒီပြဿနာကို ဖြေရှင်းဖို့ နည်းလမ်း ၃ ခု ရှိပါတယ်။

### နည်းလမ်း (၁) - `useEffect` ကို သုံးခြင်း (အကောင်းဆုံး)
React ရဲ့ `useEffect` က Client-side မှာပဲ အလုပ်လုပ်တာ ဖြစ်လို့ Hydration ပြီးမှ Data ကို ပြောင်းလဲစေပါတယ်။

```javascript
import { useState, useEffect } from 'react'

export default function MyComponent() {
  const [isClient, setIsClient] = useState(false)

  useEffect(() => {
    setIsClient(true) // Client ရောက်မှ true ပေးလိုက်မယ်
  }, [])

  return (
    <div>
      {isClient ? "Browser က Data ပြမယ်" : "Server က Data ပြမယ်"}
    </div>
  )
}
```

### နည်းလမ်း (၂) - `suppressHydrationWarning`
တကယ်လို့ မတူတာက သိပ်အရေးမကြီးဘူး (ဥပမာ- ရက်စွဲပြတာမျိုး) ဆိုရင် Warning ကို ပိတ်ထားလို့ ရပါတယ်။

```javascript
<p suppressHydrationWarning>
  {new Date().toLocaleTimeString()}
</p>
```

### နည်းလမ်း (၃) - Dynamic Import (No SSR)
အဲ့ဒီ Component တစ်ခုလုံးကို Server မှာ Render မလုပ်ခိုင်းဘဲ ကျော်သွားလို့ ရပါတယ်။

```javascript
import dynamic from 'next/dynamic'

const NoSSRComponent = dynamic(() => import('../components/Chart'), {
  ssr: false,
})
```

---

## အနှစ်ချုပ်
Hydration Error တက်တာဟာ **"Server မှာ သိတဲ့အချက်အလက် နဲ့ Browser မှာ သိတဲ့အချက်အလက် မတူလို့"** ဖြစ်တာပါ။ `useEffect` နဲ့ `isClient` state ကို သုံးပြီး Client ရောက်မှသာ Browser နဲ့ဆိုင်တဲ့ အလုပ်တွေကို လုပ်ခိုင်းတာက အသန့်ရှင်းဆုံး နည်းလမ်းဖြစ်ပါတယ်။

သင် အခုလုပ်နေတဲ့ Debt Tracker မှာကော ဘယ်နေရာမှာ ဒီ Error နဲ့ ကြုံနေရတာလဲ? (ဥပမာ- Currency Format ပြတာလား၊ ဒါမှမဟုတ် Local Storage က Data ဆွဲထုတ်တာလား?)
