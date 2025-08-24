# Salesforce Deployment

Repo ini bisa dipakai untuk melakukan deployment dinamis ke Salesforce Org.

## 🚀 Cara Pakai
1. Generate **SFDX Auth URL** dari org Salesforce kamu dengan cara login terlebih dahulu melalui VS Code dan ketikkan di terminal:
   sf org display --verbose
2. Ambil Sfdx Auth Url
3. POST ke middleware (URL: https://salesforce-middleware.onrender.com/generate) dengan format command line:
   curl -X POST https://salesforce-middleware.onrender.com/generate \
   -H "Content-Type: application/json" \
   -d '{"authUrl":"force://PlatformCLI::..."}

  dan akan mendapatkan respon:
  { "token": "abc123def456" }
4. Ambil token dan buat Pull Request dengan format bodi deskripsi:
   token: abc123def456
   target: sandbox/production
   testlevel: RunSpecifiedTests (bisa menggunakan RunLocalTests untuk run semua test class)
   testclass: MyTest1,MyTest2