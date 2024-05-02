# Criando-um-Sistema-de-Classificados-com-Ruby-on-Rails

Criando um sistema de classificados usando Ruby on Rails. Vamos dividir o projeto em módulos para facilitar o desenvolvimento e manutenção. Aqui está uma descrição geral do projeto e exemplos práticos de como implementá-lo.

### Descrição do Projeto:
O projeto consistirá em um sistema de classificados online onde os usuários podem listar itens para venda, troca ou doação. O sistema permitirá aos usuários criar anúncios, pesquisar itens, entrar em contato com os vendedores e gerenciar seus próprios anúncios.

### Funcionalidades:
- **Criação de Anúncios**: Usuários podem criar anúncios com detalhes do item, preço e fotos.
- **Pesquisa de Anúncios**: Uma funcionalidade de busca para encontrar itens específicos.
- **Gerenciamento de Anúncios**: Usuários podem editar ou excluir seus próprios anúncios.
- **Sistema de Mensagens**: Para comunicação entre compradores e vendedores.

### Módulos:
1. **Autenticação de Usuários**: Para registro e login de usuários.
2. **Modelo de Anúncios**: Para armazenar informações dos itens anunciados.
3. **Controlador de Anúncios**: Para gerenciar as requisições HTTP relacionadas aos anúncios.
4. **Interface do Usuário**: Para a criação e exibição de anúncios.
5. **Sistema de Busca**: Para permitir que os usuários pesquisem anúncios.
6. **Sistema de Mensagens**: Para permitir comunicação entre os usuários.

### Exemplo Prático - Modelo de Anúncios:
```ruby
class Ad < ApplicationRecord
  belongs_to :user
  has_many_attached :images

  validates :title, :description, :price, presence: true
end
```

### Exemplo Prático - Controlador de Anúncios:
```ruby
class AdsController < ApplicationController
  before_action :set_ad, only: [:show, :edit, :update, :destroy]

  def index
    @ads = Ad.all
  end

  def show
  end

  def new
    @ad = Ad.new
  end

  def create
    @ad = current_user.ads.build(ad_params)
    if @ad.save
      redirect_to @ad, notice: 'Anúncio criado com sucesso.'
    else
      render :new
    end
  end

  private

  def set_ad
    @ad = Ad.find(params[:id])
  end

  def ad_params
    params.require(:ad).permit(:title, :description, :price, images: [])
  end
end
```

### Testes Automatizados:
Para garantir a qualidade do software, você deve escrever testes automatizados para cada funcionalidade. Por exemplo, você pode usar RSpec para testes de modelo e Cucumber ou Capybara para testes de integração.

### Deploy em Produção:
Após o desenvolvimento e os testes, você pode fazer o deploy da aplicação no Heroku ou em outro serviço de hospedagem de sua preferência.

Essa é uma visão geral de como você pode estruturar seu sistema de classificados com Ruby on Rails.
