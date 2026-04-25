VS Code ကို Windows 10 ကနေ အစအနမကျန်အောင် (Settings တွေ၊ Extensions တွေပါကုန်အောင်) Uninstall လုပ်ပြီး Clean ဖြစ်အောင် လုပ်ဖို့က အဆင့် (၃) ဆင့်ပဲ လိုပါတယ်။ ပုံမှန် Uninstall လုပ်ရုံနဲ့တော့ Settings တွေက ကျန်နေတတ်လို့ အောက်ပါအတိုင်း သေချာလေး လုပ်ပေးပါ-

### ၁။ ပုံမှန် Uninstall အရင်လုပ်ပါ
1.  **Start Menu** ကနေ **Add or remove programs** ကို ရှာပြီး ဝင်ပါ။
2.  List ထဲမှာ **Microsoft Visual Studio Code** ကို ရှာပါ။
3.  **Uninstall** ကို နှိပ်ပြီး ပြီးဆုံးအောင် အရင်လုပ်လိုက်ပါ။

---

### ၂။ ကျန်ရှိနေတဲ့ Configuration Folder များကို ဖျက်ပါ
ဒီအဆင့်က အရေးကြီးဆုံးပါ။ ဒါမှသာ နောက်တစ်ခါပြန်တင်ရင် အဟောင်းက Settings တွေ ပြန်မပါလာမှာ ဖြစ်ပါတယ်။

* **Settings & Cache ဖျက်ရန်:**
    1.  `Windows Key + R` ကို နှိပ်ပြီး **Run** box ကို ဖွင့်ပါ။
    2.  `%AppData%` လို့ ရိုက်ထည့်ပြီး Enter ခေါက်ပါ။
    3.  ပွင့်လာတဲ့ Folder ထဲက **`Code`** ဆိုတဲ့ folder ကို ရှာပြီး **Delete** လုပ်ပစ်ပါ။

* **Extensions များ ဖျက်ရန်:**
    1.  `Windows Key + R` ကို ထပ်နှိပ်ပါ။
    2.  `%UserProfile%` လို့ ရိုက်ထည့်ပြီး Enter ခေါက်ပါ။
    3.  အဲဒီထဲက **`.vscode`** ဆိုတဲ့ folder ကို ရှာပြီး **Delete** လုပ်လိုက်ပါ။ (ဒီထဲမှာ သင်သွင်းထားတဲ့ Extensions တွေ အကုန်ရှိနေတာပါ)။

---

### ၃။ Temporary Files များကို ရှင်းထုတ်ပါ (Optional)
ပိုပြီး စိတ်ချရအောင် ပိုလျှံနေတဲ့ temporary file တွေကိုပါ ရှင်းပေးနိုင်ပါတယ်-
1.  **Run** box (`Win + R`) မှာ `%temp%` လို့ ရိုက်ပြီး Enter ခေါက်ပါ။
2.  အဲဒီထဲက folder တွေ အကုန်လုံးကို Select ပေးပြီး ဖျက်လိုက်ပါ။ (အချို့ ဖျက်မရတာတွေ ရှိရင် Skip လုပ်ပေးပါ)။

---

### 💡 Summary Checklist
| Folder Path | အကြောင်းအရာ |
| :--- | :--- |
| `%AppData%\Code` | User Settings, Hotkeys, History |
| `%UserProfile%\.vscode\extensions` | Installed Extensions |

အခုဆိုရင် VS Code က ကိုကို့စက်ထဲမှာ အသစ်စက်စက် ဝယ်ထားတဲ့စက်လိုမျိုး ဘာမှမရှိတော့ဘဲ လုံးဝ Clean ဖြစ်သွားပါပြီ။ အစကနေ ပြန်သွင်းချင်ရင်တော့ [Official Website](https://code.visualstudio.com/) ကနေ ပြန်ယူနိုင်ပါတယ်ခင်ဗျာ။
