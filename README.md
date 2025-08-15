# 📏 Calculadora de Peso Ideal (IMC)

Aplicação web simples em **React** para calcular o **IMC** e indicar se o usuário está **abaixo do peso**, **no peso ideal** ou **acima do peso** com base em **altura** e **peso**.

---

## ✅ Especificações Técnicas Obrigatórias
- Receber **altura (m)** e **peso (kg)** do usuário;
- Calcular o **IMC** usando `IMC = peso / (altura * altura)`;
- Exibir o **resultado** e a **classificação** (abaixo, ideal, acima);
- Interface simples, organizada em **componentes** reutilizáveis;
- Código utilizando **useState**, **props** e **renderização condicional**.

---

## 🛠 Tecnologias Utilizadas
- **React** (UI declarativa baseada em componentes);
- **JavaScript (ES6+)** (lógica da aplicação e manipulação de estado);
- **HTML5** (estrutura de conteúdo);
- **CSS3** (estilos e layout).

---

## 📚 O que Aprendi (baseado no método do projeto anterior)
- **Gerenciamento de Estado**: uso do hook `useState` para controlar valores de entrada e o resultado do cálculo de forma reativa;
- **Componentização**: criação e reutilização de componentes para a UI, como `Input`, `Botao` e `ResultadoIMC`;
- **Props**: passagem de dados e funções entre componentes (**pai → filho**);
- **Renderização Condicional**: exibir o resultado **somente** depois do cálculo.

---

## 🚀 Como Executar o Projeto
> Exemplo usando Vite + React (você pode adaptar para CRA, Next.js, etc.).

```bash
# 1) Criar o projeto
npm create vite@latest calculadora-peso-ideal -- --template react
cd calculadora-peso-ideal

# 2) Instalar dependências
npm install

# 3) Substituir/Adicionar os arquivos abaixo em src/ e src/components/

# 4) Rodar em desenvolvimento
npm run dev
```

Abra o endereço indicado no terminal (geralmente `http://localhost:5173`).

---

## 🗂 Estrutura sugerida
```
src/
├─ App.jsx
├─ App.css
├─ main.jsx
└─ components/
   ├─ Input.jsx
   ├─ Botao.jsx
   └─ ResultadoIMC.jsx
```

---

## 🧩 Código Essencial

### `src/components/Input.jsx`
```jsx
import React from "react";

export default function Input({ type = "text", step, placeholder, value, onChange }) {
  return (
    <input
      type={type}
      step={step}
      placeholder={placeholder}
      value={value}
      onChange={(e) => onChange(e.target.value)}
    />
  );
}
```

### `src/components/Botao.jsx`
```jsx
import React from "react";

export default function Botao({ texto, onClick, disabled }) {
  return (
    <button onClick={onClick} disabled={disabled}>
      {texto}
    </button>
  );
}
```

### `src/components/ResultadoIMC.jsx`
```jsx
import React from "react";

function classificarIMC(imc) {
  if (imc < 18.5) return "Abaixo do peso";
  if (imc <= 24.9) return "Peso ideal";
  if (imc <= 29.9) return "Acima do peso";
  return "Obesidade";
}

export default function ResultadoIMC({ imc }) {
  if (imc == null) return null; // Renderização condicional
  return (
    <div className="resultado">
      <h2>Seu IMC: {imc.toFixed(2)}</h2>
      <p>{classificarIMC(imc)}</p>
    </div>
  );
}
```

### `src/App.jsx`
```jsx
import React, { useState } from "react";
import "./App.css";
import Input from "./components/Input.jsx";
import Botao from "./components/Botao.jsx";
import ResultadoIMC from "./components/ResultadoIMC.jsx";

export default function App() {
  const [altura, setAltura] = useState(""); // em metros
  const [peso, setPeso] = useState("");     // em kg
  const [imc, setImc] = useState(null);

  const podeCalcular = () => {
    const a = parseFloat(altura);
    const p = parseFloat(peso);
    return a > 0 && p > 0;
  };

  const calcularIMC = () => {
    const a = parseFloat(altura);
    const p = parseFloat(peso);
    if (!a || !p || a <= 0 || p <= 0) return;
    const valor = p / (a * a);
    setImc(valor);
  };

  const limpar = () => {
    setAltura("");
    setPeso("");
    setImc(null);
  };

  return (
    <div className="App">
      <h1>Calculadora de Peso Ideal</h1>

      <div className="form">
        <Input
          type="number"
          step="0.01"
          placeholder="Altura em metros (ex: 1.75)"
          value={altura}
          onChange={setAltura}
        />
        <Input
          type="number"
          step="0.1"
          placeholder="Peso em kg (ex: 70)"
          value={peso}
          onChange={setPeso}
        />

        <div className="acoes">
          <Botao texto="Calcular" onClick={calcularIMC} disabled={!podeCalcular()} />
          <Botao texto="Limpar" onClick={limpar} />
        </div>
      </div>

      <ResultadoIMC imc={imc} />
    </div>
  );
}
```

### `src/App.css`
```css
.App {
  font-family: Arial, sans-serif;
  text-align: center;
  max-width: 520px;
  margin: 40px auto;
  padding: 24px;
}

.form {
  display: flex;
  gap: 8px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 16px;
}

input, button {
  padding: 10px 12px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.acoes {
  display: flex;
  gap: 8px;
  justify-content: center;
  width: 100%;
}

.resultado {
  margin-top: 16px;
  padding: 12px;
  border-radius: 8px;
  background: #f7f7f7;
}
```

---

## 🧮 Fórmula e Critérios
- **Fórmula do IMC**: `IMC = peso (kg) / (altura (m) * altura (m))`  
- **Classificação** (OMS, versão simplificada):
  - `< 18.5` → Abaixo do peso
  - `18.5 a 24.9` → Peso ideal
  - `25.0 a 29.9` → Acima do peso
  - `≥ 30` → Obesidade

> *Observação:* Esta é uma ferramenta educativa e não substitui avaliação profissional.

---

## 📝 Observação Final
Este projeto segue a mesma metodologia do **“Calculadora de Orçamento Pessoal”**, reforçando:
- **useState** para estado;
- **componentização** e **props** para organização;
- **renderização condicional** para exibição do resultado;
- uso de **HTML5/CSS3** para estrutura e estilo.

Boas práticas e melhorias futuras podem incluir: testes, acessibilidade, responsividade avançada e persistência com `localStorage`.
