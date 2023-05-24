1. **Jakie są podstawowe cechy systemu plików ext4?** ext4 (Fourth Extended Filesystem) jest popularnym systemem plików w systemie Linux. Główne cechy to:
   
- Wsparcie dla dużych woluminów danych (do 1 eksabajta) i rozmiarów plików (do 16 terabajtów).
- Journaling dla zapewnienia integralności danych.
- Dobra wydajność operacji odczytu i zapisu.
- Skuteczne zarządzanie danymi.

2. **Jakie są główne różnice między ext4 a wcześniejszą wersją ext3?** ext4 wprowadza kilka usprawnień w porównaniu do ext3, takich jak:
   
 - Większe limity rozmiarów plików i woluminów.
 - Lepsza wydajność operacji.
 - Wsparcie dla unikalnych identyfikatorów plików (UUID).
 - Journaling wielu bloków.
 - Szybsze montowanie systemu plików.

3. **Jakie są główne zalety systemu plików XFS w porównaniu do ext4?** XFS (X File System) jest rozwiniętym systemem plików, który oferuje:
   
- Wysoką wydajność w przypadku dużych woluminów danych i dużych plików.
- Skalowalność.
- Efektywne zarządzanie metadanymi.
- Wsparcie dla journalingu.
- Odtwarzanie po awarii systemu.

4. **Jakie są główne cechy systemu plików Btrfs?** Btrfs (B-tree File System) to nowoczesny system plików zaprojektowany dla systemów Linux. Główne cechy Btrfs to:
   
- Kopia zapasowa i odtwarzanie danych.
- Wsparcie dla systemu plików zrównoleglonych.
- Deduplikacja.
- Szyfrowanie.
- Kompresja.
- Snapshotty.
- Dynamiczne zarządzanie rozmiarem woluminów.

5. **Jakie są główne zastosowania Btrfs i jakie funkcje oferuje?** 
   
   Btrfs znajduje zastosowanie w różnych scenariuszach, takich jak:
   
- Przechowywanie danych.
- Serwery plików.
- Wirtualizacja.
- Tworzenie kopii zapasowych. Oferuje funkcje takie jak:
- Tworzenie i zarządzanie snapshottami.
- Klonowanie woluminów.
- Obsługę RAID.
- Kompresję danych.
- Przywracanie danych po awarii.
- Kontrolę spójności danych.

6. **Jakie są zalety systemu plików ZFS w porównaniu do innych systemów plików?** 
 
 - **Integralność danych:** ZFS zapewnia mechanizmy sum kontrolnych (checksums), które chronią integralność danych. Każdy blok danych jest sumowany i weryfikowany podczas odczytu, co pozwala wykrywać i naprawiać błędy.
- **Ochrona przed uszkodzeniami danych:** Dzięki technologii kopiowania na zapis (Copy-on-Write) ZFS tworzy kopie danych przed ich zapisaniem, co chroni przed utratą danych w przypadku awarii sprzętu lub błędów zapisu.
- **Snapshotty i klonowanie:** ZFS umożliwia tworzenie momentowych kopii zapasowych (snapshotów) danych w dowolnym momencie, co pozwala na łatwe przywracanie plików do wcześniejszych stanów. Można również tworzyć klonowane wersje cał