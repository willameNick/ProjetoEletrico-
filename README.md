# Projeto Elétrico MT/BT — APK (Capacitor)

App de projeto elétrico (postos de combustíveis e subestações particulares — Equatorial Piauí).
Web app de arquivo único (`www/index.html`) empacotado como APK com Capacitor 6.

## Gerar o APK pelo GitHub (sem instalar nada)
1. Crie um repositório no GitHub e envie **todo** o conteúdo desta pasta (incluindo `.github` e `android`).
2. Aba **Actions → Gerar APK → Run workflow** (também roda a cada push na `main`).
3. Ao terminar, baixe o artefato **ProjetoEletrico-APK** → `app-debug.apk`.
4. Copie para o celular e instale (permita "fontes desconhecidas").

## Gerar localmente
Requisitos: Node 20+, JDK 17, Android SDK.
```
npm install
npm run apk
# saída: android/app/build/outputs/apk/debug/app-debug.apk
```
Ou `npm run open` para abrir no Android Studio.

## Atualizar o app
Edite `www/index.html`, depois `npx cap sync android` (o workflow já faz isso).

## O que muda no APK em relação à página web
- **Salvar/compartilhar arquivos:** PDF, DXF, SVG e CSV abrem a folha de compartilhamento do Android (salvar em Arquivos, enviar por WhatsApp/e-mail).
- **jsPDF embutido** (`www/jspdf.umd.min.js`): o PDF funciona offline.
- **Mapa:** base OpenStreetMap e busca da rua precisam de internet; sem internet ficam só os pontos e as distâncias.
- **Supabase:** funciona (informe URL e chave na aba Saídas → Projetos).
- Permissões: internet e localização (botão "Minha localização").

## APK de loja (release assinado)
O workflow gera APK *debug*. Para a Play Store: crie um keystore, guarde-o como *secret* do GitHub e troque `assembleDebug` por `assembleRelease` com assinatura (`signingConfigs` em `android/app/build.gradle`). Nunca envie o `.keystore` ao repositório.

## Aviso técnico
As tabelas de referência (fatores de demanda, ampacidade, distâncias da NBR 14639, limite de aterramento, medição) são editáveis e devem ser conferidas nas NBRs e NDUs vigentes da Equatorial. O projeto continua sob responsabilidade do engenheiro habilitado (ART/RRT).
