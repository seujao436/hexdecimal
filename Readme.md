# U32 Little‑Endian ↔ Hex Bytes Converter

Conversor em HTML/JS que replica exatamente a lógica do print: **bytes em Hex** → **inteiro sem sinal de 32 bits (U32) em *little‑endian*** e também o caminho inverso (**U32 decimal** → **bytes em Hex** na ordem correta para *LE*).

> **Status:** MVP funcional • Front‑end puro (sem dependências) • Compatível com desktop e mobile

---

## 🚀 Demo local

Basta abrir o arquivo `index.html` no navegador. Não requer servidor nem instalação.

---

## ✨ Funcionalidades

* **HEX → Decimal (U32 • LE):** interpreta 4 bytes informados (ex.: `70 18 12 A0`) como *little‑endian* e retorna o valor decimal.
* **Decimal → HEX (bytes para LE):** dado um número U32 (0…4 294 967 295), gera:

  * **Hex para o campo de bytes** (na ordem LSB→MSB) — pronto para colar e obter o mesmo valor no modo *LE*.
  * **Hex BE convencional** (representação usual de 32 bits).
* Mostra também o **valor BE** quando você digita HEX, para comparação.
* Normaliza entradas: ignora espaços, vírgulas e `0x`.

---

## 🧠 Endianness (resumo rápido)

* **Little‑endian (LE):** o **primeiro byte** é o **menos significativo**. Se os bytes forem `AA BB CC DD` (como digitados no campo), o valor é:

  $valor = AA·256^0 + BB·256^1 + CC·256^2 + DD·256^3$

* **Big‑endian (BE):** o **primeiro byte** é o **mais significativo**:

  $valor = DD·256^0 + CC·256^1 + BB·256^2 + AA·256^3$

O app calcula **LE** (como no print) e, para referência, exibe também o **BE**.

---

## 🧪 Exemplos práticos

### 1) HEX → Decimal (LE)

* Entrada **HEX (bytes):** `701812A0`
* Bytes lidos (como digitados): `70 18 12 A0`
* **Decimal (LE U32):** `2685540464`
* **Hex BE equivalente do valor:** `A0121870`

### 2) Decimal → HEX (bytes para LE)

* Entrada **Decimal:** `2685840464`
* **Hex BE (valor convencional):** `A016AC50`
* **Bytes LE (LSB→MSB):** `50 AC 16 A0`  → para colar no campo: `50AC16A0`

> Observação: `2685540464` (caso #1) **não** é igual a `2685840464` (caso #2). A diferença é `300 000` (0x493E0), por isso os HEX resultantes mudam.

---

## 🛠️ Como usar

1. **HEX → Decimal:**

   * Cole `8` dígitos hexadecimais (ex.: `701812A0`) ou `4` bytes com/sem espaços.
   * Veja o **Decimal (LE U32)** e o **BE U32** na seção de saída.
2. **Decimal → HEX:**

   * Digite um U32 (0 a 4 294 967 295).
   * Copie o **Hex para o campo de bytes** (essa string já está na ordem *LE* para produzir o mesmo valor ao colar na primeira caixa).

---

## 📂 Estrutura do projeto

```
/ (raiz)
├── index.html   # Aplicação única (HTML + CSS + JS embutidos)
└── README.md    # Este arquivo
```

---

## 🔍 Validação manual (cálculo LE)

Para `70 18 12 A0` (hex):

```
0x70 * 256^0 =         112
0x18 * 256^1 =       6.144
0x12 * 256^2 =   1.179.648
0xA0 * 256^3 = 2.684.354.560
-----------------------------
Total (LE)       2.685.540.464
```

---

## 🧩 Roadmap

* [ ] Entrada de sequências maiores (analisar em **blocos de 4 bytes**) e listar todos os U32 LE e BE.
* [ ] Copiar/colar com formatação automática de grupos.
* [ ] Testes automatizados em navegador (Playwright).
* [ ] "Pausar" auto‑sincronização entre os campos para inspeção manual.

---

## 🤖 Desenvolvimento

É um arquivo único. Para editar:

1. Abra `index.html` no editor.
2. Use um Live Server (VS Code) **ou** apenas recarregue o arquivo no navegador.

### Principais funções (JS)

* Normalização de hex (mantém 8 dígitos; remove `0x`, espaços, vírgulas).
* Conversão **HEX → bytes (BE)**.
* Cálculo **bytes → decimal (LE e BE)** sem operadores de sinal.
* Conversão **decimal → bytes (LE)** e **decimal → hex (BE)**.

---

## ❓ FAQ

**1) Por que meu número decimal não bate com o do site?**
Verifique **endianness**. O print utiliza **U32 *little‑endian***; se você interpretar como BE, o valor muda.

**2) Posso colar `0x` ou separar com espaços?**
Sim. O app normaliza para 8 dígitos (mantendo os 4 bytes finais).

**3) Por que 2685540464 e 2685840464 são diferentes se parecem?**
A diferença é `300 000` (0x493E0), logo os bytes e o HEX resultantes também são diferentes.

---

## 📝 Licença

MIT — use livremente para estudos e trabalhos.

---

## 📎 Créditos

Projeto e especificação guiados por comparações entre **U32 LE** e **bytes em Hex** conforme print de referência do usuário.
