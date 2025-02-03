# USDA Dataset Processing

Este notebook realiza a manipulação e limpeza de dados nutricionais, combinando múltiplas fontes de dados relacionadas a alimentos e nutrientes. Ele começa renomeando colunas para padronizar a nomenclatura e realiza a fusão (merge) de diferentes DataFrames com base em identificadores comuns, como `nutrient_id` e `fdc_id`. Em seguida, os dados são pivotados para transformar nutrientes em colunas e somar valores repetidos. Após isso, é feita uma limpeza adicional, eliminando entradas vazias e verificando a conformidade dos nomes das colunas com o padrão `snake_case`. Por fim, o conjunto de dados refinado é salvo em CSV e também armazenado em um banco de dados SQL para uso posterior.

## 📂 Estrutura do Repositório

- `notebooks/` - Jupyter Notebooks para manipulação de dados  
- `data/` - Conjunto de dados utilizados  

## 🚀 Como Usar

1. **Clone o repositório**:
   ```powershell
   git clone https://github.com/jandrade-dev/USDA.git
   cd USDA
   ```

2. **Instale as dependências necessárias**:
   ```powershell
   pip install -r requirements.txt
   ```

3. ⚠️ **Configuração obrigatória: Atualizar credenciais do banco de dados**  
   Este projeto utiliza **PostgreSQL** para armazenar os dados.  
   **Antes de executar o código, você deve definir suas credenciais**.

   - 🔹 **Passo 1:** Crie um arquivo chamado **`.env`** na raiz do projeto.  
   - 🔹 **Passo 2:** Adicione suas credenciais ao arquivo `.env`, substituindo os valores pelos seus:

   ```plaintext
   DB_USERNAME=SEU_USUARIO
   DB_PASSWORD=SUA_SENHA
   DB_HOST=SEU_HOST
   DB_PORT=5432
   DB_DATABASE=SEU_BANCO
   ```

   ⚠️ **Se você não configurar esse arquivo, o código não conseguirá conectar ao banco de dados e resultará em erro.**

4. **Abra o Jupyter Notebook**:
   ```powershell
   jupyter notebook
   ```

5. **Execute os notebooks para processar os dados**.

## 🛠 Como o Banco de Dados é Carregado no Código?

O código do projeto está configurado para carregar automaticamente as credenciais do banco a partir do arquivo `.env`.  
Se necessário, verifique se este trecho está presente no código:

```python
import os
from dotenv import load_dotenv
from sqlalchemy import create_engine

# Carregar variáveis do .env
load_dotenv()

# Configuração segura do banco de dados
DATABASE_URL = f"postgresql://{os.getenv('DB_USERNAME')}:{os.getenv('DB_PASSWORD')}@{os.getenv('DB_HOST')}:{os.getenv('DB_PORT')}/{os.getenv('DB_DATABASE')}"
engine = create_engine(DATABASE_URL)
```

Esse método garante que as credenciais não fiquem expostas no código-fonte.

## 📝 Licença

Este projeto está sob a licença MIT.
