# Dzień 1 – Odpowiedzi

1. **Na jakich platformach sprzętowych można uruchomić Linuksa?**  
   - x86 (32-bit), x86_64 (64-bit), ARM (np. Raspberry Pi), PowerPC, RISC-V, MIPS.  
   - Linux jest przenośny i wspiera wiele architektur sprzętowych, w tym starsze i serwerowe.

2. **Jak wybrać odpowiednią wersję systemu Linux do swoich potrzeb?**  
   - Dla początkujących: Ubuntu, Linux Mint, Fedora Workstation.  
   - Dla zaawansowanych: Arch, Gentoo, Slackware.  
   - Dla serwerów: Debian, Ubuntu Server, RHEL, Rocky Linux.  
   - Wybór zależy od: poziomu doświadczenia, zastosowania (desktop/serwer), dostępności pakietów i wsparcia.

3. **Czym różnią się od siebie dystrybucje: RHEL, CentOS i CentOS Stream?**  
   - **RHEL (Red Hat Enterprise Linux):** komercyjna, stabilna, z płatnym wsparciem.  
   - **CentOS (do 2021):** darmowa kopia RHEL, bez wsparcia – obecnie przestarzała.  
   - **CentOS Stream:** działa jako „przyszła wersja RHEL”, dostaje aktualizacje przed RHEL, mniej stabilna od RHEL.

4. **Jak przebiega typowa instalacja systemu Linux?**  
   - Przygotowanie nośnika instalacyjnego (USB, ISO).  
   - Bootowanie z nośnika i uruchomienie instalatora.  
   - Wybór języka, klawiatury, strefy czasowej.  
   - Partycjonowanie dysku (root, swap, /home).  
   - Wybór środowiska graficznego (opcjonalnie).  
   - Ustawienie użytkownika i hasła.  
   - Instalacja pakietów i reboot.

5. **Czym jest SWAP i jakie są różnice między jego włączeniem a wyłączeniem?**  
   - SWAP to przestrzeń na dysku wykorzystywana jako awaryjna pamięć RAM.  
   - **Zalety włączenia:**  
     - System może działać przy pełnym zużyciu RAM.  
     - Może hibernować (jeśli swap = RAM).  
   - **Wyłączenie:**  
     - Mniejsza latencja, mniej zapisów na dysku SSD.  
     - Możliwość „zawieszenia się” systemu przy braku RAM.

6. **Jak dobrać odpowiedni rozmiar partycji SWAP do swojego systemu?**  
   - Ogólne zasady (dla desktopów):  
     - RAM < 2 GB → SWAP = 2x RAM  
     - RAM 4–8 GB → SWAP = RAM  
     - RAM > 16 GB → SWAP = 2–4 GB (chyba że potrzebna hibernacja)  
   - Przy hibernacji: SWAP ≥ RAM.  
   - Na serwerach i SSD stosuje się często minimalny lub brak swap.

7. **Czym różni się środowisko graficzne (Desktop Environment) od menedżera okien (Window Manager)?**  
   - **Desktop Environment (DE):** zestaw aplikacji + interfejs graficzny (GNOME, KDE, XFCE).  
   - **Window Manager (WM):** tylko zarządza oknami, lekki i szybki (i3, DWM, Openbox).  
   - DE zazwyczaj zawiera WM wewnętrznie.

8. **Jakie są główne zalety korzystania z CLI (Command Line Interface) w porównaniu do GUI?**  
   - Mniejsze zużycie zasobów.  
   - Szybkość i możliwość automatyzacji (skrypty).  
   - Zdalne zarządzanie (np. przez SSH).  
   - Dostęp do zaawansowanych narzędzi i większej kontroli.

9. **Wymień po 3 zalety i 3 wady środowiska graficznego (GUI).**  
   ✅ **Zalety GUI:**  
   - Intuicyjność dla początkujących.  
   - Łatwość obsługi programów graficznych.  
   - Multitasking z oknami, ikonami, pulpitami.  

   ❌ **Wady GUI:**  
   - Większe zużycie RAM i CPU.  
   - Nie nadaje się do minimalnych systemów lub serwerów.  
   - Mniejsza automatyzacja i trudniejsze zdalne zarządzanie.
