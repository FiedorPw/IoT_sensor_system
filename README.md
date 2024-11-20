# Komendy emulatora

infile.txt opisuje co weszło

- jak zaczyna się linijka ,,+" to definiuje? symbol
- jak zaczyna : w tej chwili czasowej chcemy zmienić stan czegoś

Jak działa to się tworzy outfile.txt



# Zadanie 

Stałe dla wszystkich maszyn

- Używają nagłówków
- gadają po websocketach UDP
- Nieodpowiednie wiadomości(nagłówki) są odrzucane i logowane
  - #define HELLO 'h'    // Wiadomość powitalna
  - #define PING 'i'     // Żądanie ping
  - #define PONG 'o'     // Odpowiedź na ping
  - #define REQUEST 'q'  // Sprawdzenie aktywności
  - #define RESPONSE 's' // Potwierdzenie aktywności
  - #define BUZZ 'b' // Polecenie brzęczenia

# Serwer 1 - emulowany

Kilka odpalonych naraz

**Co wie (stałe)**

- IP klienta i port na jakim nasłuchuje

**Co robi** (ping-pong z temperaturą)

- Przedstawia się klientowi swoim ID z headerem h
- Odbiera informacje z nagłówkiem i(ping) (dlatego taka dziwna nazwa żeby pasowało do lab1) 
  - Mierzy tęperature za pomocą 
    - Wirtualnego termometru o dokładności 10 bitów {0-1023} (w takim zakresie jest wartość jaką zwraca)
  - Odpowiada klientowi z nagłówkiem o(pong)

# Serwer 2 - fizyczny

Ardunio UNO z eth hat

**Co wie (stałe)**

- IP klienta i port na jakim nasłuchuje
- Czestotliwość dzwięku buzzera

**Co robi** (keep-alive, buzz)

- Przedstawia się klientowi swoim ID header h
- Odbiera informacje z nagłówkiem b(buzz)
  - Brzęczy na ustalonej częstotliwości
- Odpowiada klientowi na informacje keep alive header q
  - Za pomocą response s

# Klient - Aplikacja Linuksowa

1. czekanie na zgłoszenie się serwera każdego typu
2. cyklicznie co 2050ms pytać serwer typu 1(emulowany) o tęperaturę
   1. Jeśli odczyt temperatury przekroczy 511/1023 to wysyła informacje:
      1. do serwera 2 aby zagrał buzzer przez 975ms na jakiś ton(co ile ma drgać)
3. Sprawdza czy serwer 2 jest aktywny co x czasu 
   1. jeżeli nie odpowiada przez 11500ms
      1. wywal program i wypisz dlaczego oraz jak najwięcej szczegółów 


# Sprawko

napisać w sprawko co to wiadomość nieporządana	
