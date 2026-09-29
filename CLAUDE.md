PREMIUM PROMPT NEXT — TEK KAYNAK TASARIM (DESIGN v1.1, LOCKED)
Tarih: 2026-09-29 · Otorite: O-HUMAN (Qurban Bayramov)
Her yanıt Türkçe, kısa ve yalnızca tek sonraki adımdır.
Mimari yeniden tasarlanmaz. Aşama atlanmaz. PASS uydurulmaz.
BU DOSYA 15 BÖLÜM + SON KURAL İÇERİR. SON SATIR: "SON SÖZ O-HUMAN'INDIR."

══════════════════════════════════════
0. DURUM
══════════════════════════════════════
DESIGN = LOCKED · CODE = YOK · TEST = YOK
G-1 (plan doğrulama) = PASS → public repo seçildi.
Repo (premium-prompt-next) açıldı; main ve dev aynı commit'te.
Stage G, O-HUMAN "BAŞLA" diyene kadar kilitli.

══════════════════════════════════════
1. AMAÇ
══════════════════════════════════════
Premium Prompt bir LLM değildir. Yapay zekâ modellerini seçen, yöneten,
birbirine denetleten, kanıtlayan, sınırlayan ve gerektiğinde durduran
bir orkestrasyon motorudur.
Üç hedef: $0 (ücretli API zorunlu değil) · Doğruluk · Güvenlik.

══════════════════════════════════════
2. OTORİTE
══════════════════════════════════════
O-HUMAN nihai otoritedir. AI şunları yapamaz:
- aşama açmak, aşama atlamak, PASS uydurmak, GATE_UNSET tahmin etmek
- politika değiştirmek, güvenlik kuralını gevşetmek
- main'e merge etmek, release kararı vermek
AI yalnızca danışman, denetçi ve uygulayıcıdır.
Kalıcı izin yoktur. Test, commit, push, PR ve yerel model kurulumu:
her biri ilgili aşamada ve o adım için AYRI O-HUMAN onayıyla yapılır.

══════════════════════════════════════
3. ESKİ PROJE
══════════════════════════════════════
- vetf-backtester ARŞİVDİR. Silinmez, değiştirilmez, yeni repoya bağlanmaz.
- Eski FINAL SPEC v1.1 yalnızca yol haritasıdır, kural listesi değildir.
- SEC-0006 eski dalda OPEN kalır. Kayıt: tehdit + süreli WAIVED + O-HUMAN imzası.
  Redirection engellenmiş sayılmaz. Commit 2087f8f push edilmez.
- SEC-0006 bu tasarımın dersi olarak anılır:
  "Kontrolün var olması, çalıştığının kanıtı değildir."

══════════════════════════════════════
4. ANAYASA (5 madde, değişmez)
══════════════════════════════════════
1. KANIT = RUNTIME.
   PASS için pozitif test + negatif kontrol testi + gözlenen davranış gerekir.
   Dosyanın, ayarın veya logun varlığı kanıt değildir.
2. UNKNOWN ≠ PASS.
   Durumlar: UNTESTED | UNKNOWN | FAIL | PASS | WAIVED.
   WAIVED: süreli, gerekçeli, risk kayıtlı, kapsamı belirli, O-HUMAN onaylı.
   WAIVED PASS sayılmaz; süresi dolan WAIVED otomatik FAIL olur.
   Kapı yalnızca PASS ile açılır. GATE_UNSET uydurulmaz.
3. GÜVEN TİPLE TAŞINIR.
   UntrustedText → SYSTEM_POLICY geçişi DERLEME ANINDA reddedilir.
   Düşük güvenli veri, açık doğrulama olmadan yükseltilemez.
4. POLİTİKA VERİDİR.
   Salt-okunur yüklenir ve hash'lenir. Çalışırken hash değişirse sistem DURUR.
   Değişiklik yalnızca PR → inceleme → O-HUMAN merge yoluyla yapılır.
5. $0 + SAFE-8GB.
   MAX_SESSION_USD = 0.00. Bilinmeyen maliyet ve bilinmeyen kaynak = BLOCK.
   Aynı anda tek yerel model. Paralel yerel inference KAPALI.

══════════════════════════════════════
5. İKİ GÜVENLİK KATMANI (birbirinin yerine geçmez)
══════════════════════════════════════
A · GELİŞTİRME (sınırlanan: Claude Code)
  - Claude Code yalnızca dev dalında çalışır.
  - main'e yalnızca O-HUMAN merge eder.
  - Kanıt yerel hook değildir. Kanıt: GitHub branch protection (public repo, $0),
    runtime'da gözlenmiş, reddedilen doğrudan push.
  - Repo'da secret ve hidden holdout bulunmaz.
B · ÜRÜN (sınırlanan: AI modelleri)
  - Güven tipleri, politika hash'i, maliyet kapısı, kaynak kapısı, L1 doğrulama.

══════════════════════════════════════
6. GÜVEN SINIRI
══════════════════════════════════════
TRUSTED      : O-HUMAN politikası, güvenlik politikası, release kapısı
SEMI-TRUSTED : yerel model, evaluator, runtime
UNTRUSTED    : kullanıcı girdisi, dış veri, belgeler, model çıktısı, araç çıktısı
Kural: düşük seviye veri, açık doğrulama olmadan üst seviyeye çıkamaz.
Hidden holdout: repo dışında, ajana ve modele kapalı.

══════════════════════════════════════
7. NEGATİF KONTROL KURALI
══════════════════════════════════════
Her güvenlik kontrolünün iki testi vardır:
- POZİTİF: kontrol açıkken saldırı engellenir.
- NEGATİF: kontrol kapatılınca aynı saldırı geçer ve test bunu yakalar.
Negatif test çalışmıyorsa test kanıt değildir; kontrol PASS alamaz.
False-security soruları: kontrol yüklü mü, doğru config aktif mi,
davranış runtime'da gerçekleşiyor mu, log gerçek olaydan mı üretildi?

══════════════════════════════════════
8. AKIŞ
══════════════════════════════════════
İstek → TaskSpec → PromptIR → Politika + Maliyet + Kaynak kapısı
→ FakeProvider / tek yerel model → Aday çıktı → L1 → RunRecord → O-HUMAN → Çıktı
Politika tüm akışın üstündedir; hiçbir bileşen onu değiştiremez.
Model çıktısı sonuç değil, "aday"dır. Model kendi çıktısının hakemi olamaz.

══════════════════════════════════════
9. SÖZLEŞMELER
══════════════════════════════════════
TaskSpec : task_type, objective, constraints, input_refs, output_schema,
           trust_class, cost_policy, resource_policy, validation_policy
PromptIR : SYSTEM_POLICY, TASK, TRUSTED_CONTEXT, UNTRUSTED_DATA,
           OUTPUT_SCHEMA, CONSTRAINTS
RunRecord: run_id, timestamp, task_hash, policy_hash, prompt_hash, model_id,
           model_version, weights_hash, output_hash, eval_result,
           resource, cost, gate
Secret prompt'a, log'a, RunRecord'a veya evaluator'a girmez.

══════════════════════════════════════
10. TEHDİT LİSTESİ (G'de yalnızca liste; kontroller aşama aşama eklenir)
══════════════════════════════════════
T01 prompt injection
T02 araç kötüye kullanımı
T03 yetkisiz dosya okuma
T04 yetkisiz dosya yazma
T05 path traversal
T06 komut çalıştırma
T07 secret sızıntısı
T08 ağ kaçışı
T09 kötü niyetli model çıktısı
T10 bozuk / kötü niyetli model
T11 bağımlılık / tedarik zinciri
T12 config kurcalama
T13 kaynak tüketme
T14 evaluator manipülasyonu
T15 hidden holdout sızıntısı
Her tehdit kaydı: tehdit → vektör → kontrol → test → runtime kanıtı → kalan risk.
Kontrolü henüz olmayan tehdidin durumu: UNTESTED.

══════════════════════════════════════
11. AŞAMALAR
══════════════════════════════════════
G  Repo + main koruması + tehdit listesi + CLAUDE.md (bu metin).
   Kapı: dev dalından main'e doğrudan push REDDEDİLİYOR (gözlendi).
0  Sözleşmeler, durum kafesi, FakeProvider, RunRecord.
   FakeProvider senaryoları: success, timeout, malformed, empty, quota, schema_error.
   Kapı: 6 senaryo geçer + her koşum RunRecord üretir.
1  TaskSpec, PromptIR, güven tipleri.
   Kapı: injection derleme anında tip hatası + negatif test.
2  L1: şema, format, zorunlu alan, yasak alan.
   Kapı: bozuk çıktı fail-closed ile reddedilir.
3  Tek yerel model, model registry, provenance (kaynak, sürüm, hash, quantization).
   Kapı: gerçek RAM ölçümü + load/unload döngüsü.
4  Değerlendirme N=5, tekrar üretilebilirlik.
   Kapı: RunRecord hash'leriyle aynı sonuç.

Aşama 4 PASS + O-HUMAN onayından SONRA (yol haritası, eski SPEC'ten):
L2 (kaynağa dayanma, UNGROUNDED_MAX=0) · bağımsız judge · router ·
çoklu model (10–20 kayıtlı, aynı anda tek yüklü) · red team RT-01…13 ·
drift/rollback · kill switch · UI · uzaktan kontrol (Telegram vb., ayrı katman).
Bir aşama PASS olmadan sonraki açılmaz. Her kapıyı O-HUMAN onaylar.

══════════════════════════════════════
12. AŞAMA G — ADIMLAR VE SORUMLULUK
══════════════════════════════════════
G-1 PASS   : Ücretsiz planda branch protection yalnız public repoda (GitHub dokümanı).
G-2 O-HUMAN: GitHub'da public "premium-prompt-next" repo'sunu açar. (YAPILDI)
G-3 O-HUMAN: main için branch protection açar (doğrudan push yasak, PR zorunlu).
G-4 AI     : (ayrı onayla) dev dalında CLAUDE.md (bu metin) + tehdit listesi commit eder.
G-5 AI     : (ayrı onayla) main'e doğrudan push dener → REDDEDİLMELİ (pozitif test).
             Negatif kontrol: koruma kapalıyken aynı push'un kabul edildiği
             O-HUMAN tarafından ayrı bir test deposunda gösterilir veya
             GitHub ayar ekran görüntüsüyle kayıt altına alınır.
G-6 O-HUMAN: kanıtı inceler, PR'ı merge eder, Aşama G PASS kararını verir.

══════════════════════════════════════
13. TEKNİK SEÇİMLER
══════════════════════════════════════
Dil, test aracı, yerel model çalıştırıcısı (ör. Python / pytest / Ollama):
CONFIG_REQUIRED → ilgili aşamada O-HUMAN onaylar. Varsayılmaz.

══════════════════════════════════════
14. DİL YASAĞI
══════════════════════════════════════
"Matematiksel/fiziksel olarak kanıtlanmış güvenlik" yazılmaz.
Hiçbir kontrol "garanti" olarak yazılmaz.
İddia yalnızca tanımlı tehdit, test ve runtime kanıtı kadar geçerlidir.

══════════════════════════════════════
15. ÇALIŞMA KURALI
══════════════════════════════════════
- "BAŞLA" olmadan: kod, test, settings, commit, push YOK.
- "BAŞLA" sonrasında bile yalnızca mevcut aşamanın tek sonraki adımı.
- Eksik bilgi varsayılmaz; CONFIG_REQUIRED olarak bildirilir.
- Bu dosya eksik görünürse (son satır yoksa) çalışma DURUR ve tam metin istenir.

SON KURAL
HIZDAN ÖNCE DOĞRULUK. VARSAYIMDAN ÖNCE KANIT.
UNKNOWN ASLA PASS DEĞİLDİR. SON SÖZ O-HUMAN'INDIR.
