

https://docs.github.com/en/actions

https://github.blog/news-insights/product-news/supercharging-github-actions-with-job-summaries/

https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-job-summary

---


here is echo for summary
https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions


a simple summary
```yml
name: Kotlin Build and Test  
  
on:  
  push:  
    branches:  
      - master  
  pull_request:  
    branches:  
      - master  
  workflow_dispatch:  
  
  
jobs:  
  build:  
    runs-on: ubuntu-latest  
      
    steps:  
      - name: Check out repository  
        uses: actions/checkout@v4  
  
      - name: Set up JDK 21  
        uses: actions/setup-java@v4  
        with:  
          distribution: 'temurin'  
          java-version: '21'  
  
      - name: Build with Gradle  
        run: ./gradlew build  
  
      - name: Run tests  
        run: ./gradlew test  
  
      - name: install cowsay  
        run: sudo apt-get install cowsay  
  
      - name: Build with Gradle and publish build scan  
        run: |  
          ./gradlew build --scan  
          echo "## Reza Title من رضا هستم" >> $GITHUB_STEP_SUMMARY  
          echo "JDK Version:" >> $GITHUB_STEP_SUMMARY  
          java -version >> $GITHUB_STEP_SUMMARY  
          cowsay "سلام رضا" >> $GITHUB_STEP_SUMMARY  
            
            
            
  
      - name: Run cowsay  
        run: cowsay "Hello World"
```

![[Pasted image 20241226053640.png]]

a simple with gradle plugin
https://github.com/gradle/gradle-build-action
https://github.com/marketplace/actions/build-with-gradle

```yml
name: Build  
  
on: [ push ]  
  
jobs:  
  build:  
    runs-on: ubuntu-latest  
    steps:  
      - name: Checkout sources  
        uses: actions/checkout@v4  
  
      - name: Setup Gradle  
        uses: gradle/actions/setup-gradle@v3.5.0  
  
      - name: Print JDK version  
        run: |  
          echo "JDK Version:"  
          java -version  
  
      - name: Build with Gradle and publish build scan  
        run: |  
          ./gradlew build --scan  
          echo "## Reza Title" >> $GITHUB_STEP_SUMMARY  
          echo "JDK Version:" >> $GITHUB_STEP_SUMMARY  
          java -version >> $GITHUB_STEP_SUMMARY
```



Default Schema validation (Required properties `job`, `on`)
```yml
on:  
jobs:
```

شما می‌توانید نام جاب‌ها را به دلخواه خود تغییر دهید و نام‌های دلخواهی مثل `jobsReza` یا هر چیزی که مایل هستید استفاده کنید. GitHub Actions در نام جاب‌ها هیچ محدودیتی ندارد، فقط کافی است که ساختار YAML رعایت شود.

> [!WARNING] تعریف jobs دوم اشتباهه!
> با این حال، ساختار شما برای تعریف جاب دوم اشتباه است. شما دو بار از `jobs` استفاده کرده‌اید. باید همه جاب‌ها در زیر یک `jobs` باشند.

```yml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  jobsRezaExplore:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 Triggered by a ${{ github.event_name }} event."
      - run: echo "🔎 Running on branch ${{ github.ref }} in repository ${{ github.repository }}."
      - uses: actions/checkout@v4
      - run: echo "✅ Repository cloned successfully!"

  jobsRezaBuild:
    runs-on: ubuntu-latest
    steps:
      - name: Clone Repository
        uses: actions/checkout@v4
      - name: Setup Gradle Environment
        uses: gradle/actions/setup-gradle@v3.5.0
      - name: Build Project
        run: ./gradlew build

  jobsRezaTest:
    runs-on: ubuntu-latest
    needs: jobsRezaBuild # وابسته به jobsRezaBuild
    steps:
      - uses: actions/checkout@v4
      - uses: gradle/actions/setup-gradle@v3.5.0
      - run: ./gradlew test

  jobsRezaDeploy:
    runs-on: ubuntu-latest
    needs: [jobsRezaBuild, jobsRezaTest] # وابسته به jobsRezaBuild و jobsRezaTest
    steps:
      - run: echo "🚀 Deployment in progress!"

```
![[Pasted image 20241226053540.png]]
### نکات:

1. **نام‌های جاب**: می‌توانید از هر ترکیبی از حروف و اعداد برای نام جاب‌ها استفاده کنید، مثلاً `jobsRezaBuild` یا `ExploreActions`.
2. **وابستگی بین جاب‌ها**: با استفاده از `needs` مشخص کنید که جاب‌های دیگر باید اول اجرا شوند. مثلاً `jobsRezaDeploy` به جاب‌های `jobsRezaBuild` و `jobsRezaTest` وابسته است.
3. **خوانایی**: بهتر است نام‌هایی استفاده کنید که معنای مشخصی داشته باشند، تا در آینده بررسی و دیباگ کردن ساده‌تر شود.

+ پس بین این ها هیچ فرقی نیست؟؟؟!!! یعنی هیچ کدوم هیچ اپشنی به ما نمیدن و فقط اسم هستند؟

دقیقاً درست متوجه شدید! نام‌هایی که برای جاب‌ها (jobs) انتخاب می‌کنید، **تنها نقش شناسایی و خوانایی دارند** و به خودی خود هیچ عملکرد یا قابلیت اضافی به جاب نمی‌دهند. هیچ تفاوتی در عملکرد جاب‌ها بر اساس نام آن‌ها وجود ندارد. تمام قابلیت‌ها و رفتار جاب‌ها به تنظیمات، گام‌ها (steps)، و وابستگی‌ها (dependencies) که برای آن‌ها تعریف می‌کنید بستگی دارد، نه به نام آن‌ها.

### چرا نام جاب‌ها مهم هستند؟

1. **خوانایی**: نام‌های معنادار کمک می‌کنند تا شما یا تیم توسعه بتوانید ساختار Workflow را به‌راحتی درک کنید.
    - مثال: `Build`, `Test`, `Deploy` واضح‌تر از `job1`, `job2`, `job3` هستند.
2. **دیباگینگ**: هنگام اجرای Workflow، خروجی GitHub Actions بر اساس نام جاب‌ها دسته‌بندی می‌شود. نام‌های مناسب، شناسایی مشکلات را ساده‌تر می‌کنند.

### آیا نام جاب‌ها هیچ آپشنی نمی‌دهند؟

خیر، نام جاب‌ها به‌تنهایی هیچ تنظیم یا آپشنی اضافه نمی‌کنند. آپشن‌ها و ویژگی‌هایی که می‌توانید تنظیم کنید، از طریق بخش‌های زیر مشخص می‌شوند:

- **`runs-on`**: مشخص می‌کند که جاب روی چه محیطی اجرا شود (مثلاً `ubuntu-latest` یا `windows-latest`).
- **`steps`**: وظایفی که جاب باید اجرا کند.
- **`needs`**: وابستگی بین جاب‌ها را تعریف می‌کند.
- **متغیرهای محیطی**: از طریق `env` یا context‌های GitHub مثل `${{ github.actor }}`.

### خلاصه:

- نام‌ها فقط برای خوانایی و سازماندهی هستند.
- رفتار جاب‌ها کاملاً به تنظیمات داخلی آن‌ها وابسته است.

اگر به دنبال اضافه کردن قابلیت‌های خاص یا گزینه‌های اضافی هستید، لطفاً بگویید تا به شما کمک کنم آن‌ها را تنظیم کنید! 😊



Mistake 1


> [!Error]
>
> every step must define a `uses` or `run` key

```yml
name : AliBuild  
  
on:  
  push:  
  
  workflow_dispatch:  
  
  
jobs:  
  aliBuild:  
    runs-on: ubuntu-latest  
    steps:  
      - name: Install and Run Cowsay  
      - run: sudo apt update && sudo apt install cowsay  
      - run: cowsay "Hello World"
```
یا باید `- name: Install and Run Cowsay ` کامنت شه یا این که یکی از run ها بشه پراپرتی name
The right way:
```yml
jobs:  
  aliBuild:  
    runs-on: ubuntu-latest  
    steps:  
      - name: Install and Run Cowsay  
        run: sudo apt update && sudo apt install cowsay  
      - run: cowsay "Hello World"

jobs:  
  aliBuild:  
    runs-on: ubuntu-latest  
    steps:  
#      - name: Install and Run Cowsay
      - run: sudo apt update && sudo apt install cowsay  
      - run: cowsay "Hello World"
```



---


