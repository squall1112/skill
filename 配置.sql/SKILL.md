---
name: fake-data-generator
description: 根据国家/公会/玩家数量，自动生成 t_guild + t_user 的 SQL 配置文件。支持20国文化适配命名。
---

# 配置.sql - 本地机器人预置数据生成器

根据国家/公会/玩家数量，自动生成 `t_guild` + `t_user` 的 SQL 配置文件。

---

## 表结构（必须严格对齐）

### t_guild
```sql
INSERT INTO `t_guild` (`id`, `name`, `country_code`, `fake`, `member_capacity`, `member_count`) VALUES (?, '?', '?', true, ?, ?);
```

### t_user
```sql
INSERT INTO `t_user` (`id`, `nickname`, `country_code`, `fake`) VALUES (?, '?', '?', true);
```

---

## 支持的国家（20个）

`AR, AU, BR, CA, CH, CN, DE, ES, FR, IN, IT, JP, KR, MX, NL, NO, RU, SE, TR, US`

---

## 命名规则

### 1. 玩家昵称（核心原则：网络中玩家真正会取的名字）

**两种格式，8:2 随机分配：**
- **文化特色词**（80%）：食物/物品/形容词/网络用语，各国风格不同
- **Player_XXXXXX**（20%）：固定前缀 + 6位数字字母（`ABCDEFGHJKLMNPQRSTUVWXYZ23456789`，不含 I/O/0/1）

#### 各国文化特色词库

| 国家 | 风格 | 示例 |
|------|------|------|
| US | 英文单词/组合词 | Marshmallow, Bubble, Pickle, Nacho, Bacon, Flamingo, Nugget, Tater, Avocado |
| CN | 中文网络用语/美食梗 | 芋泥波波, 干饭人, 摸鱼怪, 沙威玛, 疯狂星期四, 内卷达人, 躺平大师, 社恐患者, 氪金大佬 |
| JP | 平假名/片假名可爱词 | めたんこ, にゃんこ, たこ焼き, ふわふわ, ぷにぷに, ぼよよん, もぐもぐ |
| KR | 韩语词/网络用语 | 라면, 치킨, 김치, 보라, 감자, 참치, 딸기, 햄스터, 뭐해, 꿀잼 |
| DE | 德语词/复合词 | Brezel, Schnitzel, Brötchen, Wurst, Keks, Schoki, Klopapier, Sauerteig, Kartoffel |
| FR | 法语/食物/俚语 | Baguette, Croissant, Fromage, Bof, Chelou, Wesh, Kifer, Câline, Tabernac |
| ES | 西班牙语/食物/俚语 | Tortilla, Paella, Flamenco, Chulo, Guay, Nene, Bicho, Tapas, Fideo, Gazpacho |
| IT | 意大利语/食物/俚语 | Pasta, Carbonara, Ciao, Mamma, Pizza, Gnocco, Spritz, Figata, Bello |
| BR | 葡萄牙语/食物 | Pao, Queijo, brigadeiro, acai, caipirinha, pudim, coxinha, empada, vatapa, quindim |
| AR | 西班牙语/食物 | Chorizo, Tacos, Pollo, Quesadilla, Chimichurri, Alfajor, Empanada, Dulce, Burrito, Enchilada |
| AU | 英文/澳式英语 | Avocado, Brekkie, Barbie, Arvo, Chocky, Bikkie, Maccas, Servo, Esky, Heaps |
| CA | 英法混合/枫糖 | Maple, Syrup, Timbit, Beaver, Canoe, Lumber, Pancake, Tundra, Eh, Aboot |
| CH | 德语/罗什德语 | Brötli, Schoggi, Velo, Alpage, Chuchi, Meringue, Spitz, Nidle, Poschte, Raclette |
| IN | 印地语/英语混合 | Chai, Butter, Masala, Gully, Laddu, Bhai, Jugaad, Koi, Nahi, Mast, Samosa |
| MX | 西班牙语/食物/俚语 | Chilaquiles, Nopal, Elote, Guacamole, Pozole, Taco, Salsa, Mote, Camote, Huarache |
| NL | 荷兰语/食物 | Poffertjes, Kroket, Oliebol, Stamppot, Drop, Gezellig, Borrel, Boter, Kaas |
| NO | 挪威语/食物/俚语 | Fjord, Brus, Kose, Leken, Snill, Koselig, Flink, Bruse, Tur, Greit |
| RU | 俄语/食物 | Blin, Pirozhki, Pelmeni, Borscht, Smetana, Syrniki, Varennik, Kvass, Kefir, Chak |
| SE | 瑞典语/食物/俚语 | Fika, Kanelbulle, Mys, Lagom, Mamma, Finfin, Flum, Banan, Keso, Skit |
| TR | 土耳其语/食物 | Simit, Pide, Lahmacun, Döner, Lokum, Kaymak, Börek, Çay, Aşk, Hayat |

### 2. 公会名（网游玩家真实公会风格 + 强烈文化适配）

**命名特征：**
- 2-3个英文/本国语单词组合
- 常见元素：食物、动物、职业、形容词
- 避免中文拼音、避免真实姓名

#### 各国公会名库

| 国家 | 风格示例 |
|------|---------|
| US | BubbleBusters, PizzaPals, SunsetSippers, SockMonkeys, MemeMakers, DinoHuggers, PajamaSquad, BaconBrigade, LootGoblins, AFKLegends, PotatoSquad, PepperoniPirates, TacoTuesday, GummyBears, NachoNinjas, LaggyLegends, WipeItGood, Murlocalypse, GnomeDepot, BaconAvengers |
| CN | 火锅突击队, 奶茶上分团, 王者摸鱼队, 沙威玛传奇, 干饭人联盟, 内卷无限公司, 躺平事务所, 氪金不眨眼, 社恐互助会, 摸鱼大师, 疯狂星期四, 炸鸡快乐屋, 小龙虾战队, 柠檬精本精, 咸鱼翻身营, 摸鱼天团, 氪金大佬窝, 社畜俱乐部, 打工人联盟, 峡谷摸鱼帮 |
| JP | たこ焼き隊, にゃんこ部屋, お=Mayん同好会, ひまわり組, たまごだまし, ゆりかご連, あまおう狩り, ゆるキャラ部, たぬき工房, まるまる村, ふわふわ牧場, もぐもぐ会, ぷにぷに村, ぼよよん軍団, めにゃこ殿, かにかに亭, さかな亭, いぬごん屋敷, ねこまる堂, うさぎもち本舗 |
| KR | 라면파티, 어묵탐험대, 빙수전사, 김치해적단, 불닭모둠, 삼겹살도사, 치킨영웅, 붕어싸제, 호떡왕국, 만두군단, 감자태터, 참치캔, 딸기농장, 보라매듭, 햄스터돌, 라면은삶는다, 치킨은바삭, 김치는삶아, 불닭은매워, 삼겹은기름 |
| DE | KäsekrainerKrew, BienenstichBuddies, Bretzeldörfer, WaldfeeWelt, BiergartenBandits, Marmeladenmäuse, KaminfeuerKollegen, WurstRitter, BretzelStolz, KartoffelKinder, SchnitzelSpäher, OberGrenze, KlopapierKönig, SauerteigSquad, Gemütlichkeit |
| FR | CroqueMonsieur, MacaronSquad, TartTatinTeam, BaguetteBuddies, FromageFous, CaféCrmeCrew, ChocolatChaud, CrêpeCarnival, BofBrigade, ChelouSquad, WeshWarriors, CâlinePatrol |
| ES | TortillaSquad, PaellaKings, FlamencoForce, ChuloCrew, GuayGuerreros, NeneNacion, BichoBros, TapasTribe, FideoForce, GazpachoGang, ChorizoSquad, JamonHeroes, PatatasBravas, BurritoBros, QuesadillaKrew |
| IT | PastaPatrol, CiaoCrews, MammaMia, PizzaPunks, GnoccoForce, SpritzSquad, FigataFellows, CarbonaraKlan, RisottoRaiders, LasagnaLegion, TiramisuTeam, EspressoElite |
| BR | PaoDeQueijo, BrigadeiroGang, AcaiWarriors, CoxinhaCrew, PudimPower, CaipirinhaKings, EmpadãoElite, VatapaForce, QuindimQuest, BeijuBros, TapiocaTown, CanjicaCrew |
| AR | TacosLocos, ChorizoSquad, AlfajorArmy, EmpanadaElite, ChimichurriKings, FideoForce, DulceDreams, PolloGrande, QuesadillaCrew, BurritoBros, EnchiladaEmpire, NachosLoco, GuacamoleGang |
| AU | BushrangerBoys, VegemiteSquad, BoomerangBand, OutbackLegion, SunsetSippers, ChokkieBites, ArvoAdventures, BarbieBoys, MaccasCrew, EskyLegends, AvocadoArmy, BrekkieBros, TimTamSlam |
| CA | MapleSyrup, TimbitSquad, BeaverBros, CanoeCrew, LumberLegends, PancakePatrol, TundraWarriors, FlagFlyers, EhBros, CanoeKings, TimbitArmy, BeaverTail, MapleLeaf |
| CH | BrötliBund, SchoggiKreis, VeloClub, AlpageAces, ChuchiCrew, MeringueMafia, SpitzSquad, NidleNinjas, ChrapfKinder, PoschtePower, RacletteRitter, FondueFellows, RöstiRaiders |
| IN | ChaiWalas, ButterChicken, MasalaMafia, GullyGang, LadduLegends, BhaiBros, JugaadJunta, KoiClub, NahiNinjas, MastMunchies, SamosaSquad, PakoraPatrol, NaanWarriors |
| MX | ChilaquilesCrew, NopalNinja, EloteEmpire, GuacGang, PozolePatrol, TacoTuesday, SalsaSquad, MoteMafia, CamoteCrew, HuaracheHeroes, GorditaGuard, SopeSquad, TamalTornado |
| NL | PoffertjesParad, KroketKrew, OliebolOlijf, StamppotStrijd, DropDroom, GezelligGang, BoterBazen, KaasKoning, BorrelBazen, KroketKoning, OliekoekOrde, StroopwafelSquad |
| NO | FjordFighter, BrusBrus, KoseKlan, LekenLegends, SnillSquad, KoseligKrew, FlinkFolk, BruseBrors, TurTropp, GreitGutta, KrumkakeKlan, LefseLiga, FårikålFolk |
| RU | BlinBrigade, PirozhkiPatrol, PelmeniPals, BorschtBoys, SmetanaSquad, SyrnikiSquad, VarennikVikings, KvassKlan, KefirKrew, ChakChampions, OlivierOrden, ShchiSquad |
| SE | FikaFellows, KanelbulleKlan, MysMän, LagomLag, MammaMia, FinfinFolk, FlumFlam, BananBoys, KesoKings, SkitSquad, KroppkakorKlan, JanssonsJakt |
| TR | SimitSquad, PidePatrol, LahmacunLords, DönerDreams, LokumLegion, KaymakKlan, BörekBros, ÇayCrew, AşkAslanlari, HayatHarmani, KuruFasulye, İmamBayıldı, DolmaDefenders |

---

## 生成流程

### Step 1：询问用户需求

必须确认以下参数，**提问时必须告知范围**：

| 参数 | 提问方式 | 示例 |
|------|---------|------|
| 国家列表 | "需要哪些国家？" | 全部20国 / AR,US,CN,JP / 自定义 |
| 每国公会数 | 范围随机 → **告知用户会在范围内随机** | 例如：4-7个（我会随机）/ 固定5个 |
| 每公会成员数 | 范围随机 → **告知用户会在范围内随机** | 例如：30-50人（我会随机）/ 固定40人 |
| 特殊要求 | 是否有种子数/ID范围等 | 可选 |

> **关键**：当用户选择范围时，必须明确告知「我在这个范围内随机取值」，不要让用户以为会是固定值。

### Step 2：生成数据

1. 用固定种子保证可复现（默认 seed=42，或用户指定）
2. 为每个国家生成公会（公会名不重复）
3. 为每个公会生成玩家（80%文化特色词 + 20% Player_格式）
4. 组装 SQL

### Step 3：输出

```sql
-- Fake Data SQL Dump

START TRANSACTION;

-- Guilds
INSERT INTO `t_guild` ...;

-- Users
INSERT INTO `t_user` ...;

COMMIT;
```

---

## 注意事项

1. **真实姓名禁止出现**——玩家昵称必须是网络用语风格（食物/物品/形容词）
2. **公会名要文化适配**——根据国家使用对应语言风格
3. **格式严格对齐**——使用 backtick 包裹表名/字段名
4. **公会id从1递增，用户id从10000递增**
5. **member_capacity = member_count**（满员公会）
