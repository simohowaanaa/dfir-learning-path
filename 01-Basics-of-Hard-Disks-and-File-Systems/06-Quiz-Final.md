# Quiz final — Basics of Hard Disks and File Systems

Résultat : réussi, badge obtenu.

## Questions et réponses

**Q1. What feature of SSDs makes them more resistant to physical shocks?**
→ **The absence of moving parts.**

**Q2. Which of the following is incorrect for the FAT32 file system?**
→ **The maximum file size it supports is 8TB.** (incorrect — la limite réelle est 4 Go pour la taille de fichier ; 8 To est la limite théorique de partition, pas de fichier)

**Q3. Which feature of the NTFS file system improves data integrity and system recovery?**
→ **Journaling**

**Q4. Which attribute is not stored by the NTFS file system?**
→ **MountHistory** (n'existe pas parmi les attributs NTFS réels : `$OBJECT_ID`, `$SECURITY_DESCRIPTOR`, etc.)

**Q5. Which file system is specifically designed for portable storage devices such as flash drives and SD cards?**
→ **exFAT**

**Q6. Which file system used in Linux operating systems offers journaling features?**
→ **EXT3** (EXT2 n'a pas de journaling ; FAT32/exFAT ne sont pas des systèmes de fichiers Linux natifs)

**Q7. Which ZFS file system feature checks data and metadata for corruption?**
→ **Checksums and Self-Healing**

**Q8. Which file system has a journaling system to reduce data loss and ensure quick recovery after crashes?**
→ **XFS**

**Q9. Which feature of the SquashFS file system saves disk space?**
→ **High Compression Ratio**

**Q10. Which of the following is true for tmpfs?**
→ **It uses system memory.**
