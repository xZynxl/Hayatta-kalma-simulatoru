#include <stdio.h>  // Klavye ve ekran islemleri icin
#include <stdlib.h> // Rastgele sayi (rand) icin
#include <time.h>   // Zaman (time) fonksiyonu icin

// --- GLOBAL DEGISKENLER ---
int saglik = 100;       // Can (0-100)
int enerji = 100;       // Enerji (0-100)
int yemek_sayisi = 5;   // Baslangic yemek miktari
int siginak_durumu = 0; // 0: Yok, 1: Var
int ilerleme_puani = 0; // Puan

// --- YARDIMCI FONKSIYON: Sinirlari Kontrol Et ---
void durum_sinirla() {
    if (saglik > 100) saglik = 100;
    if (saglik < 0) saglik = 0;
    if (enerji > 100) enerji = 100;
    if (enerji < 0) enerji = 0;
    if (yemek_sayisi < 0) yemek_sayisi = 0;
}

// --- YARDIMCI FONKSIYON: Durumu Goster ---
void sadece_durumu_yazdir() {
    printf("\n--- Mevcut Durum ---\n");
    printf("Saglik: %d/100\n", saglik);
    printf("Enerji: %d/100\n", enerji);
    printf("Yemek: %d\n", yemek_sayisi);
    printf("Siginak: %s\n", siginak_durumu ? "Var" : "Yok");
    printf("Puan: %d\n", ilerleme_puani);
    printf("--------------------\n");
}

// --- KOMUT ISLEYICI FONKSIYON ---
void komut_isleyici(char komut) {
    // Degiskenler
    int bulunan_yemek;
    int tehlike_suresi;
    int i;
    int kayip;
    int kacis_faktoru = 0;
    char tahmin;
    char sifre;

    switch (komut) {
        
        // --- A: AVLAN (Enerji harca, Yemek bul, Risk al) ---
        case 'A': case 'a':
            if (enerji >= 15) { 
                enerji -= 15; // Enerji harcanir
                
                // %70 sansla yemek bulunur
                if (rand() % 10 < 7) { 
                    bulunan_yemek = (rand() % 3) + 1;
                    yemek_sayisi += bulunan_yemek;
                    printf(">> Av basarili! %d adet yemek buldunuz.\n", bulunan_yemek);

                    // Yaralanma Riski (MANTIKSAL OPERATORLER)
                    // Sanssizsan VEYA (Enerjin az VE Siginagin yoksa)
                    if ((rand() % 5 == 0) || (enerji < 10 && siginak_durumu == 0)) { 
                        saglik -= 5;
                        printf("!! Av sirasinda ufak bir kaza gecirdiniz (-5 Saglik).\n");
                    }
                } else {
                    printf(">> Av basarisiz. Yemek bulunamadi.\n");
                }
            } else {
                printf("!! Avlanmak icin enerjiniz (15) yetersiz.\n");
            }
            break;

        // --- S: SIGINAK BUL (Enerji harca, Sansa bagli bul) ---
        case 'S': case 's':
            if (siginak_durumu == 1) { // Siginak varsa dinlen
                enerji += 15; 
                saglik += 7;
                printf(">> Siginaginizda guvenle dinlendiniz (Enerji+, Saglik+).\n");
            } else { // Yoksa ara
                if (enerji >= 10) { 
                    enerji -= 10;
                    if (rand() % 5 == 0) { // %20 sans
                        siginak_durumu = 1;
                        printf(">>> TEBRIKLER! Bir siginak BULUNDU.\n");
                    } else {
                        printf(">> Siginak aramasi sonucsuz kaldi.\n");
                    }
                } else {
                    printf("!! Siginak aramak icin enerjiniz (10) yetersiz.\n");
                }
            }
            break;

        // --- R: DINLEN (GUNCELLENDI: Zarar verme kaldirildi) ---
        case 'R': case 'r':
            // Eger yemek varsa: Ye ve cok dinlen
            if (yemek_sayisi >= 1) { 
                yemek_sayisi -= 1; 
                enerji += 30;      
                saglik += 15;      
                printf(">> Yemek yediniz ve guzelce dinlendiniz. (Enerji+30, Saglik+15)\n");
            } else { 
                // Eger yemek yoksa
                enerji += 15; // Yine de enerji artar
                saglik += 5;  // Az da olsa saglik artar
                printf(">> Yiyecek yok ama dinlenip guc topladiniz. (Enerji+15, Saglik+5)\n");
            }
            break;
            
        // --- E: ENVANTER ---
        case 'E': case 'e':
            sadece_durumu_yazdir(); 
            break;
            
        // --- F: TEHLIKE SIMULASYONU (FOR Dongusu) ---
        case 'F': case 'f':
            printf("!! Tehlike simulasyonu basliyor...\n");
            tehlike_suresi = (rand() % 4) + 2; 
            printf("!! %d tur surecek bir tehlike dalgasi!\n", tehlike_suresi);
            
            {
                for (i = 1; i <= tehlike_suresi; i++) { 
                    printf("   [Tur %d]: ", i);
                    kacis_faktoru = 0;
                    
                    // Siginak ve Enerji hasari azaltir
                    if (siginak_durumu == 1) { kacis_faktoru += 5; printf("[Siginak] "); }
                    if (enerji > 50) { kacis_faktoru += 3; printf("[Enerjik] "); }
                    
                    kayip = 10 - kacis_faktoru; 
                    if (kayip < 3) kayip = 3;   
                    
                    saglik -= kayip;     
                    enerji -= kayip / 2; 
                    printf("Hasar: -%d, Enerji: -%d\n", kayip, kayip/2);
                    
                    durum_sinirla();
                    if (saglik <= 0) break; 
                }
            } 
            break;
            
        // --- P: SIFRELI KAPI (DO-WHILE Dongusu) ---
        case 'P': case 'p':
            sifre = (rand() % 10) + '0'; // Rastgele 0-9 arasi sifre
            
            printf("!! Kilitli Kapi! Gecmek icin 0-9 arasi sifreyi bulun.\n");
            
            do {
                printf(">> Tahmininiz: ");
                scanf(" %c", &tahmin);
                
                if (tahmin != sifre) {
                    printf("!! YANLIS! Tekrar deneyin.\n");
                    enerji -= 2; // Sadece enerji azalir (stres)
                    printf("(Enerji -2)\n");
                    if (enerji <= 0) break;
                }
            } while (tahmin != sifre); 

            if (enerji > 0) {
                printf(">>> DOGRU! Kapi acildi.\n");
                ilerleme_puani += 20;
                enerji -= 10;
                printf(">> Ilerleme Puani +20.\n");
            }
            break;
        
        // --- X: CIKIS ---
        case 'X': case 'x':
            printf(">> Cikis yapiliyor...\n");
            break;

        default: 
            printf("!! Gecersiz komut!\n");
            break;
    }
    
    durum_sinirla();
    
    // NOT: Bu genel aclik kuralidir. Dinlenmekten bagimsizdir.
    // Hic yemek kalmazsa karakter yavasca gucsuzlesir.
    if (yemek_sayisi == 0) { 
        saglik -= 5; 
        printf("!! Stokta yemek olmadigi icin acliktan hasar aldiniz (-5 Saglik).\n");
    }
}

// --- MAIN FONKSIYONU ---
int main() {
    char komut;
    srand(time(NULL)); 

    printf("--- C Dilinde Karakter Tabanli Hayatta Kalma Simulatoru ---\n");
    printf("Amac: Hayatta kalmak ve puan toplamak.\n");

    sadece_durumu_yazdir(); 

    do { 
        if (saglik <= 0) { 
            printf("\n!!! OYUN BITTI (Saglik Tukendi) !!!\n");
            break; 
        }

        printf("\nKomut (A/S/R/E/F/P/X): ");
        if (scanf(" %c", &komut) != 1) break;

        komut_isleyici(komut); 

    } while (komut != 'X' && komut != 'x'); 

    printf("\n--- OYUN SONA ERDI. Toplam Puan: %d ---\n", ilerleme_puani);

    return 0;
}
