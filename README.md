# Έλεγχος micro:bit-robot από Raspberry Pi με χρήση Computer Vision
---
### Εισαγωγή – Σενάριο:
Βρισκόμαστε στο έτος 2300 μ.Χ. Ο πληθυσμός της γης αυξήθηκε ραγδαία και ομάδες ανθρώπων κατάφεραν να μετοικήσουν σε απομακρυσμένους πλανήτες. Είμαστε στον πλανήτη Α-3225 και συγκεκριμένα στην **Αποβάθρα Επιβίβασης Επιβατών** με προορισμό τον γειτονικό πλανήτη Β-3225. Η μετακίνηση γίνεται με **Μη Επανδρωμένα Διαστημικά Οχήματα**, τα οποία ελέγχονται από το **Διαστημικό Κέντρο Ελέγχου Οχημάτων**. Το Κέντρο αυτό είναι υπεύθυνο για να επιτηρεί και να κατευθύνει τα  μη επανδρωμένα οχήματα στον προορισμό τους.

### Α. Περιγραφή Μακέτας (Αποβάθρα Επιβίβασης Επιβατών - Ανεφοδιασμού )
Σε επιφάνεια από διάφανο υλικό (plexi glass), τοποθετούνται σειρές από ταινίες LED (NeoPixels) έτσι ώστε να δημιουργούνται πολλαπλοί φωτεινοί διάδρομοι για την κίνηση ενός micro:bit-robot. Όταν μία συγκεκριμένη ομάδα LED είναι σε λειτουργία, το micro:bit-robot προχωράει “διαβάζοντας” τη διαδρομή που βρίσκεται μπροστά του. Σβήνοντας αυτή την συγκεκριμένη ομάδα από LED και ανάβοντας μια άλλη ομάδα LED, κατευθύνουμε το micro:bit-robot σε επιλεγμένα σημεία της μακέτας. Με αυτόν τον τρόπο δημιουργείται επιλεκτικά μια φωτεινή γραμμή κάτω από τη διάφανη μακέτα, την οποία γραμμή μπορεί να ακολουθεί το micro:bit-robot.

![Μακέτα-1](/images/Μακέτα-1.png) ![Μακέτα-3](/images/Μακέτα-3.png) ![Μακέτα-4](/images/Μακέτα-4.png) ![Μακέτα-5](/images/Μακέτα-5.png) ![Μακέτα](/images/Μακέτα.png)

### Β. Περιγραφή micro:bit-robot (Μη Επανδρωμένο Διαστημικό Όχημα)
Το robot θα κατασκευαστεί χρησιμοποιώντας ως βάση (σασί) ένα απλό CD. Ως κινητήρες θα έχει δύο servo motors (full rotation), την πλακέτα micro:bit ως ελεγκτή, μπαταρίες, δύο τροχούς και έναν infrared αισθητήρα με την δυνατότητα να “διαβάζει” τους φωτεινούς διαδρόμους των LED.

### Γ. Περιγραφή του Raspberry Pi  (Διαστημικό Κέντρο Ελέγχου Οχημάτων)
Το Raspberry Pi θα είναι εξοπλισμένο με μια απλή web camera. Θα έχει εγκατεστημένο το λογισμικό OpenCV (Computer Vision). Η camera θα έχει τοποθετηθεί ψηλά, έτσι ώστε να έχει οπτική επαφή (κάτοψη) ολόκληρης της μακέτας. Το Raspberry Pi θα έχει τη δυνατότητα μέσω του OpenCV, να αναγνωρίζει ανά πάσα στιγμή τη θέση του micro:bit-robot πάνω στη μακέτα, γνωρίζοντας εάν βρίσκεται στη επιθυμητή πορεία του ή όχι.

**Σενάριο 1:**
Το Raspberry Pi μπορεί να ελέγχει το άναμμα συγκεκριμένων ομάδων από ταινίες LED, οι οποίες βρίσκονται μπροστά από το micro:bit-robot. Το Raspberry Pi γνωρίζοντας τη θέση του robot, ενεργοποιεί την συγκεκριμένη ομάδα ταινιών LED που βρίσκονται ακριβώς μπροστά του και το όχημα τα ακολουθεί. Έτσι το Raspberry Pi καθοδηγεί το micro:bit-robot σε επιλεγμένα σημεία της μακέτας.

**Σενάριο 2:**
Η μακέτα δεν θα είναι εξοπλισμένη με ταινίες LED ούτε θα έχει σχεδιασμένο κάποιο είδος διαδρομής επάνω της. Παρόλα αυτά, στο Raspberry Pi θα έχει δοθεί μια εικόνα της μακέτας και ένα σχέδιο με μια συγκεκριμένη διαδρομή, ως αρχείο jpeg. Γνωρίζοντας λοιπόν τη θέση του  micro:bit-robot πάνω στη μακέτα με τη βοήθεια Computer Vision, το Raspberry Pi συγκρίνει τη θέση αυτή με την εικόνα της διαδρομής που του έχει ήδη φορτωθεί. Ως αποτέλεσμα μπορεί να γνωρίζει εάν το  micro:bit-robot βρίσκεται νοητά εντός ή εκτός της επιθυμητής διαδρομής. Εάν είναι εκτός, τότε το Raspberry Pi θα στείλει στο micro:bit-robot μέσω bluetooth (Η πλακέτα  micro:bit μπορεί να επικοινωνεί με άλλες συσκευές χρησιμοποιώντας Blootooth (BLE)), την εντολή να στρίψει κατάλληλα ώστε να μπει εντός της διαδρομής. Με αυτόν τον τρόπο το Raspberry Pi καθοδηγεί το micro:bit-robot στη μακέτα, σύμφωνα με το σχέδιο διαδρομής που κάθε φορά του έχει δοθεί σε αρχείο εικόνας.

---
### Λίστα Υλικών (Hardware)
* 1 Πλακέτα micro:bit
* 2 Servo-motors πλήρης περιστροφής ή 2 απλοί servo κινητήρες όπου θα τροποποιηθούν σε πλήρης περιστροφής
* 1 Αισθητήρας υπερύθρων (για χρήση ως line follοwer)
* 3 μέτρα Addressable LED Strip RGB
* 1 Raspberry Pi 3 Model B 
* 1 Web camera
* 1 φύλλο plexiglass 1x1,52m
---
