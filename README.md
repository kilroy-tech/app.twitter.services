# app.twitter.services
Beefy contract and utility services

## How to calculate Beefy positions

mooToken balances only increase/decrease on deposit/withdraw; the number of underlying (e.g. LP) tokens they represent changes over time. for standard vaults you can convert mooTokens (aka shares) to the underlying (aka want) by:

underlying amount = shares * price per full share - https://discord.com/channels/755231190134554696/758368074968858645/1260911619563716608

then you can convert underlying token amount to $ using the prices api and oracleId from vault config - https://discord.com/channels/755231190134554696/758368074968858645/1268539034901282837

---

ppfs = 1077710305111557296 / 1e18 = 1.077710305111557296 (getPricePerFullShare has 18 decimals)
usdc = 600 * 1e6 = 600000000 (USDC has 6 decimals)
shares = 600000000/1.077710305111557296 = 556735884 (integer division)

---

you need to look at `oracle` and `oracleId` of the vault config
for `oracle`:
`tokens` -> <https://api.beefy.finance/prices>
`lps` -> <https://api.beefy.finance/lps>

then find `oracleId` in response of above

so for `venus-bnb`:  oracle is tokens so fetch /prices, and oracleId is BNB, so look up BNB price, and multiply by getPricePerFullShare


3471533912775986189 / 1e18 * balance = 2721.4152694897