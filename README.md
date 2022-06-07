# Autorizador Ana Costa saúde
</br></br></br>


## Troca de Informações padrão TISS/ANS
### Solicitação de Procedimentos `Padrão TISS 3.03.03`

#### O Manual em PDF foi baixado direto do site da ANS [link direto para página](http://www.ans.gov.br/images/stories/Plano_de_saude_e_Operadoras/tiss/Padrao_tiss/manual_comunicacao_seguranca.pdf) 

Elegibilidade / autorização de procedimentos

</br></br></br></br></br>

## Troca de informações por JSON

### Verificação de  Elegibilidade

Link para acesso ao verificador de elegibilidade deve ser informado pela operadora
<!--http://agendaweb.anacosta.com.br/api/autorizador.aspx/Elegibilidade-->


> Parâmetros de entrada JSON:



````
{
  codigoPrestadorNaOperadora: '',
  numerocarteira: '',
  sequencialTransacao: '',
  loginPrestador: '',
  senhaPrestador: '',
  registroANS: '',
  dataOperacao: ''
}
````


> Especificação parâmetros de entrada



| atributo                   |   obrigatório   | tipo         |  descrição   |
| ---------------------------|-----------------|--------------|--------------|
| codigoPrestadorNaOperadora | Opcional        | alfanumérico |              |
| numerocarteira             | Obrigatório     | alfanumérico | |
| sequencialTransacao        | Obrigatório     | numérico     | sequencial criado pela prestadora para controle interno (passar 0 "zero" se a prestadora optar por não ter esse controle)|
| loginPrestador             | não implementado|              | |
| senhaPrestador             | não implementado|              | |
| registroANS                | Opcional        | numérico     | |
| dataOperacao               | Obrigatório     | Data/Hora    | Data e hora da solicitação no formato **dd/mm/aaaa hh:mm** |



> Formato da resposta JSON:


````
{
  dataRegistroTransacao: '',
  numeroCarteira: '',
  codigoPrestadorNaOperadora: '',
  sequencialTransacao: '',
  tipoTransacao: '',
  motivo: '',
  respostaSolicitacao: '',
  versao: '',
  senha: '',
}
````


> Especificação resposta:



| atributo                   |   obrigatório   | tipo         |  descrição   |
| ---------------------------|-----------------|--------------|--------------|
| dataRegistroTransacao      | Obrigatório     | Data/Hora    |  Data e hora da solicitação no formato **dd/mm/aaaa hh:mm** |
| numeroCarteira             | Obrigatório     | alfanumérico | |
| codigoPrestadorNaOperadora | Opcional        | alfanumérico | |
| sequencialTransacao        |                 |              |Retorna o mesmo passado pela prestadora para controle interno |
| tipoTransacao              |                 | alfanumérico | para elegibilidade retorna sempre **VERIFICA_ELEGIBILIDADE** |
| motivo                     |                 | alfanumérico | Se a resposta for negativa **N** retorna descrição do motivo |
| respostaSolicitacao        | Obrigatório     | alfanumérico | S/N - **S** para elegível **N** para não elegível |
| versao                     |                 | alfanumérico | versão da API |
| senha                      | Obrigatório     | alfanumérico | sequencia de caracteres gerados para validar a solicitação |


## Exemplo de acesso com ajax ( jquery )


### OBS: 
> A resposta vai estar encapsulada em um objeto "d" ( não sei porque motivo, coisa da Microsoft nessa versão ), então a variável de retorno irá recuperar a informação
desta forma:

````
var objetoValido = response.d;
````

````
  var dado = {  
      numerocarteira: 'XXXX123456789',      
      codigoPrestadorNaOperadora: '55555',      
      dataOperacao: "11/11/1111 11:11",      
      sequencialTransacao: "123",      
      loginPrestador: "",      
      senhaPrestador: "",      
      registroANS: ""      
  };
  
  $.ajax({
      url: http://url.da.api,
      data: JSON.stringify(dado),
      type: "POST",
      contentType: "application/json; charset=utf-8",
      dataType: "json",
      success: function (response) {
          if (response) {
              $('#retornaExemplo').text(JSON.stringify(response.d));
          } else {
              $('#retornaExemplo').html('Não retornou nada');
          }
      },
      error: (function Error(request) {
          $('#retornaXMLExemplo').html('ERROR text: ' + request.responseText + '\r\nDADOS: ' + JSON.stringify(dado));
      })  
  });
````
