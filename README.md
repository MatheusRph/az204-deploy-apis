# **Deploy de APIs no Azure - Guia Completo (Baseado na Certificação AZ-204)**

Neste guia, vamos detalhar como fazer o **deploy de APIs no Azure** utilizando o **Azure App Service** e o **Azure API Management (APIM)**, ambos muito usados em soluções de desenvolvimento no Azure. Este guia é ideal para quem está se preparando para a certificação **AZ-204: Developing Solutions for Microsoft Azure**.

### **Pré-requisitos**

Antes de começar, você precisará de:

- Uma **conta no Azure** (você pode usar uma conta gratuita)
- **Visual Studio** ou **VS Code** instalado
- **Azure CLI** ou **Azure PowerShell** instalados em sua máquina
- **Postman** ou ferramenta similar para testar a API após o deploy
- **.NET SDK** instalado (para quem for usar APIs em C#)

### **Passo 1: Criar e Preparar o Projeto de API**

#### 1.1. **Criar o Projeto de API no Visual Studio**
1. Abra o **Visual Studio**.
2. Crie um novo **Projeto** e escolha **ASP.NET Core Web API**.
3. Selecione a versão **.NET 6** ou **.NET 7** (certifique-se de que o seu Visual Studio está atualizado).
4. Clique em **Criar** e forneça um nome para o seu projeto, como `MyApiApp`.
5. No template de API, a opção **"Enable OpenAPI support"** pode ser ativada para fornecer documentação da API automaticamente.

#### 1.2. **Testar a API Localmente**
1. Clique em **F5** para iniciar o projeto localmente.
2. Abra o **Postman** ou seu navegador e faça uma solicitação GET para `http://localhost:5000/api/values` (ou qualquer outro endpoint que você tenha configurado) para garantir que a API está funcionando corretamente.

### **Passo 2: Criar o Azure App Service para Hospedar a API**

O **Azure App Service** oferece uma plataforma totalmente gerenciada para hospedar APIs web.

#### 2.1. **Criar o App Service no Portal Azure**
1. Acesse o **Portal Azure** (https://portal.azure.com/).
2. No menu lateral, clique em **Criar um recurso**.
3. Na busca, digite **App Service** e clique em **Criar**.
4. Preencha os seguintes campos:
   - **Assinatura**: Escolha sua assinatura.
   - **Grupo de recursos**: Crie um novo ou use um existente.
   - **Nome do App Service**: Escolha um nome exclusivo para a sua API.
   - **Publicar**: Selecione **Código**.
   - **Runtime**: Escolha o runtime do .NET (por exemplo, **.NET 6**).
   - **Região**: Escolha uma região próxima de seus usuários.
5. Clique em **Revisar + Criar** e depois em **Criar**.

#### 2.2. **Configuração de Planos de App Service**
- Durante a criação, você será solicitado a escolher um **Plano de Serviço**. Para fins de teste ou desenvolvimento, um plano **F1 (Gratuito)** pode ser suficiente.
- Para produção, considere planos mais robustos, como **P1V2**.

### **Passo 3: Fazer o Deploy da API para o Azure App Service**

#### 3.1. **Publicar a API do Visual Studio**
1. No **Visual Studio**, clique com o botão direito do mouse no projeto da API e selecione **Publicar**.
2. Escolha **Azure** como destino e clique em **Azure App Service (Windows)**.
3. Faça login com sua conta do Azure.
4. Escolha o **App Service** que você criou anteriormente.
5. Clique em **Concluir** e depois em **Publicar**. O Visual Studio fará o deploy da API para o Azure App Service.

#### 3.2. **Verificar o Deploy**
Após a publicação ser concluída, o **Visual Studio** abrirá automaticamente o navegador para o endpoint da API na URL do Azure App Service. Você pode testar a API diretamente do navegador ou usar o Postman para fazer chamadas à API.

### **Passo 4: Configurar o Azure API Management (APIM)**

O **Azure API Management** (APIM) é um serviço que permite gerenciar, proteger e analisar suas APIs.

#### 4.1. **Criar um API Management no Azure**
1. No Portal Azure, clique em **Criar um recurso**.
2. Busque por **API Management** e clique em **Criar**.
3. Preencha os seguintes campos:
   - **Assinatura**: Escolha sua assinatura.
   - **Grupo de recursos**: Use o mesmo grupo de recursos onde você criou o App Service.
   - **Nome**: Escolha um nome único para o serviço.
   - **Região**: Selecione a mesma região onde o App Service foi criado.
4. Clique em **Revisar + Criar** e depois em **Criar**.

#### 4.2. **Configurar a API no API Management**
1. Após a criação do serviço **APIM**, vá para a página de detalhes do serviço.
2. Na seção **APIs**, clique em **Adicionar API**.
3. Selecione a opção **Web API** e, em seguida, insira a URL do seu **Azure App Service**.
4. Adicione as configurações necessárias, como **Rotas** e **Policies**.
5. Clique em **Criar**.

#### 4.3. **Testar a API no APIM**
1. Acesse o painel de **APIs** no **API Management**.
2. Clique na API que você criou e utilize o **Console de Testes** para fazer chamadas e verificar a resposta.
3. Você verá a resposta da API que foi enviada através do **API Management**.

### **Passo 5: Configuração de Segurança da API (Opcional)**

Para proteger sua API, você pode usar autenticação e controle de acesso.

#### 5.1. **Adicionar Autenticação ao API Management**
1. No portal do **API Management**, navegue até **APIs**.
2. Selecione a API que você criou e vá para **Políticas**.
3. Adicione uma política de **autenticação**. Você pode usar, por exemplo, o **OAuth2**, **JWT** ou **API Key**.
4. Salve as configurações.

### **Passo 6: Monitoramento e Análise**

#### 6.1. **Habilitar Monitoramento no API Management**
1. No **Portal Azure**, acesse seu **API Management** e vá para **Insights**.
2. Ative o **Application Insights** para monitorar o desempenho e as falhas da API.
3. Você pode visualizar métricas como **latência** e **taxa de erro** da API.

#### 6.2. **Configuração de Logs**
1. Em **Logs** no API Management, você pode configurar alertas e salvar os logs para análise posterior.

### **Passo 7: Testar a API**

Agora que a API está no Azure, você pode usá-la em seu **Postman** ou diretamente no navegador. A URL será algo como:

```plaintext
https://<nome-do-app-service>.azurewebsites.net/api/values
