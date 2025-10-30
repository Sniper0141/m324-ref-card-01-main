# Doku Auftrag GitHub CI/CD

- Altes Repo als ZIP heruntergeladen.

![repo-old](image.png)


- Git initalisiert

![git-init](image-1.png)


- GitHub Repo erstellt:

![repo-new](image-2.png)


- Lokales Repo auf GitHub gepusht:

![local-repo-push](image-3.png)


- Folgendes Yaml File im Folder `./.github/workflows` geschrieben, und gepusht:
```yaml

name: MyFlow

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
          cache: 'maven'     
      - name: Build & Test
        run: mvn -B -ntp verify
      - name: Deploy
        run: mvn -B -ntp deploy
```

- Leider hat die Pipeline einen Fehler:

![error-pipeline](image-4.png)


- Der Fehler sagt, die falsche Java-Version sei benutzt worden. Ich korrigiere das Java-Version im Yaml von 11 auf 17 und pushe das Ganze nochmals. Build und Test funktioniert jetzt, aber etwas anderes funktioniert jetzt nicht:

![deploy-failed](image-5.png)


- 