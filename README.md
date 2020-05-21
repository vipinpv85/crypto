# crypto

various bugs and fixes as part of crypto


ZUC:
```
--- a/ciphers/zuc/src/zuc/sso_zuc.c
+++ b/ciphers/zuc/src/zuc/sso_zuc.c
@@ -540,7 +540,7 @@ __attribute__((gnu_inline)) inline  void sso_zuc_eia3_1_buffer(uint8_t *pKey,

     bitOffset = lengthInBits%32;        /* The bit position offset into the 32-bit word */
     wordOffset = lengthInBits/32;       /* 32-bit word offset */
-    T ^= (pZuc[wordOffset]<<bitOffset) | (pZuc[wordOffset+1]>>(32-bitOffset));
+    T ^= (pZuc[wordOffset]<<bitOffset) | (uint32_t)(((uint64_t)pZuc[wordOffset+1])>>(32-bitOffset));

     /* save the final MAC-I result */
     *pMacI = __builtin_bswap32(T ^ pZuc[L-1]);
```
