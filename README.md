# Autorizador Ana Costa saude

### Elegibilidade

O acesso ao verificador de elegibilidade será pelo link:
http://agendaweb.anacosta.com.br/api/autorizador.aspx/Elegibilidade

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

- **codigoPrestadorNaOperadora** - Opcional - alfanumérico
- **numerocarteira** - Obrigatório - alfanumérico
- **sequencialTransacao** - Obrigatório - numérico - sequencial criado pela prestadora controle interno (passar 0 "zero" se a prestadora optar por não ter esse controle)
- **loginPrestador** - não implementado
- **senhaPrestador** - não implementado
- **registroANS** - Opcional - numérico
- **dataOperacao** - Obrigatório - Data e hora da solicitação no formato **dd/mm/aaaa hh:mm**


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
- **dataRegistroTransacao** - Obrigatório - Data e hora da solicitação no formato **dd/mm/aaaa hh:mm**
- **numeroCarteira** - Obrigatório - alfanumérico
- **codigoPrestadorNaOperadora** - Opcional - alfanumérico
- **sequencialTransacao** - Retorna o mesmo passado pela prestadora para controle interno
- **tipoTransacao** - alfanumérico - para elegibilidade retorna sempre **VERIFICA_ELEGIBILIDADE**
- **motivo** - alfanumérico - Se a resposta for negativa **N** retorna descrição do motivo
- **respostaSolicitacao** - alfanumérico - S/N - **S** para elegível **N** para não elegível
- **versao** - alfanumérico - versão da API
- **senha** - alfanumérico - sequencia de caracteres gerados para validar a solicitação
