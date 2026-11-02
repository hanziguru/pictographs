# Pictograph file naming — the decoding convention

Every asset for one character derives from a single **stem**:

    stem = <pinyin_num>                      if that pinyin+tone is unique in the set
    stem = <pinyin_num>-<codepoint>          if two or more characters share the pinyin+tone

- `pinyin_num`: the character's HSK headword reading in lowercase ASCII
  with the tone as a digit 1-5 (ma3, nv3). The letter ü is written `v`
  (女 = nv3). No tone marks, no spaces.
- `codepoint`: the character's Unicode code point in lowercase hex,
  no `U+` prefix, no leading zeros (工 = 5de5, 弓 = 5f13).
- The suffix is all-or-nothing per group: if a pinyin+tone collides,
  EVERY character in the group carries its suffix. A plain stem
  therefore always means "unique in the set".

Assets per character (base: https://cdn.jsdelivr.net/gh/hanziguru/pictographs@main/):

    card  (share image, text baked in) : pictograph-<stem>.webp
    art   (drawing only, no text)     : art/<stem>-art.webp
    thumb (400px card thumbnail)      : thumbs/<stem>-thumb.webp

Worked examples:

    马 mǎ  unique      -> pictograph-ma3.webp, art/ma3-art.webp, thumbs/ma3-thumb.webp
    工 gōng collides   -> pictograph-gong1-5de5.webp
    弓 gōng collides   -> pictograph-gong1-5f13.webp
    雨 yǔ collides x3  -> pictograph-yu3-96e8.webp (羽 yu3-7fbd, 予 yu3-4e88)

## Authoritative decode table

`manifest.json` in this repo is the authoritative mapping: one row per
character with fields char, trad, pinyin, pinyin_num, gloss, hsk,
category, depicts, file, thumb, art (+ byte sizes). A consumer should
look the character up in the manifest rather than re-deriving names;
the derivation rule above exists so the convention is transparent and
auditable, and so a filename alone can be decoded back to
(pinyin_num, codepoint?) without the table.

## Collision groups (complete)

- `ba1`: 八 (-516b), 巴 (-5df4)
- `dong1`: 东 (-4e1c), 冬 (-51ac)
- `er2`: 儿 (-513f), 而 (-800c)
- `gong1`: 工 (-5de5), 弓 (-5f13)
- `jin1`: 斤 (-65a4), 巾 (-5dfe)
- `li4`: 力 (-529b), 立 (-7acb)
- `mao2`: 毛 (-6bdb), 矛 (-77db)
- `mu4`: 目 (-76ee), 木 (-6728)
- `shen1`: 身 (-8eab), 申 (-7533)
- `sheng1`: 生 (-751f), 升 (-5347)
- `shou3`: 手 (-624b), 首 (-9996)
- `xi1`: 西 (-897f), 夕 (-5915)
- `xin1`: 心 (-5fc3), 辛 (-8f9b)
- `yu3`: 雨 (-96e8), 羽 (-7fbd), 予 (-4e88)

All other 107 pinyin+tone values in the set are unique and use the plain stem.
