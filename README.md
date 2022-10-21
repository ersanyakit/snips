```
# snips

import Vibrant from 'node-vibrant'
import { hex } from 'wcag-contrast'
import { shade } from 'polished'

async function getColorFromToken(token: Token): Promise<string | null> {
  const path = `https://raw.githubusercontent.com/trustwallet/assets/master/blockchains/ethereum/assets/${token.address}/logo.png`

  return Vibrant.from(path)
    .getPalette()
    .then((palette) => {
      if (palette?.Vibrant) {
        let detectedHex = palette.Vibrant.hex
        let AAscore = hex(detectedHex, '#FFF')
        while (AAscore < 3) {
          detectedHex = shade(0.005, detectedHex)
          AAscore = hex(detectedHex, '#FFF')
        }
        return detectedHex
      }
      return null
    })
    .catch(() => null)
}
```
