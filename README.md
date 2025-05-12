*************************************************************************************************************
  *******************************************  STM32H7-EXTI  **********************************************

*************************************************************************************************************
***********************************  STM32- H753ZI - MICROCONTROLADOR  ************************************************************
*************************************************************************************************************

# Projeto de Pisca-Pisca com STM32

Este projeto demonstra um controle básico de LEDs (verde, amarelo e vermelho) em uma placa de microcontrolador STM32. O pisca dos LEDs é acionado por uma interrupção gerada pela pressão de um botão azul.

## Descrição

O código em `main.c` configura o clock do sistema, inicializa os pinos GPIO para os LEDs como saída e o pino do botão azul como entrada. Uma interrupção externa (EXTI) é configurada para ser disparada quando o botão azul é pressionado (na borda de descida).

Quando a interrupção ocorre, uma flag (`flag`) é definida como 1. No loop principal (`while(1)`), o programa verifica o valor dessa flag. Se a flag for 1, os LEDs verde, amarelo e vermelho são alternados (ligados e desligados), e a flag é resetada para 0. Isso faz com que os LEDs pisquem a cada vez que o botão é pressionado.

O projeto utiliza a biblioteca Low-Layer (LL) da STM32 para acesso direto aos periféricos, oferecendo maior controle e potencialmente melhor desempenho em comparação com a HAL (Hardware Abstraction Layer).

## Componentes Utilizados

* **Microcontrolador STM32**: A placa STM32 utilizada (o modelo específico não está detalhado no código, mas é compatível com a biblioteca LL).
* **LEDs**: LEDs nas cores verde, amarelo e vermelho conectados a pinos de saída do STM32. As definições dos pinos (por exemplo, `LED_GREEN_Pin`, `LED_GREEN_GPIO_Port`) devem estar definidas nos arquivos de cabeçalho do projeto (possivelmente em `main.h`).
* **Botão Azul**: Um botão conectado a um pino de entrada do STM32. A interrupção é configurada para este pino (`BLUE_BUTTON_Pin` no port `BLUE_BUTTON_GPIO_Port`).
* **Resistores (Opcional)**: Resistores em série com os LEDs para limitar a corrente.
* **Ferramentas de Desenvolvimento STM32**: STM32CubeIDE ou outra ferramenta compatível para compilar, fazer o upload e depurar o código.

## Estrutura do Código

* **`main.c`**: Contém a lógica principal do programa, incluindo a inicialização do sistema, a configuração dos GPIOs, a configuração da interrupção externa e o loop principal que controla o pisca dos LEDs.
* **Arquivos de Cabeçalho (`.h`)**: Podem existir arquivos de cabeçalho (como `main.h`) que definem constantes, estruturas e protótipos de funções utilizados no projeto.

## Configuração

1.  **Hardware**: Conecte os LEDs aos pinos de saída do STM32 através de resistores limitadores de corrente (se necessário). Conecte o botão azul a um pino de entrada do STM32. Certifique-se de configurar os pinos corretos no código (ou nos arquivos de cabeçalho).
2.  **Software**:
    * Abra o projeto em sua ferramenta de desenvolvimento STM32 (por exemplo, STM32CubeIDE).
    * Verifique e ajuste as definições dos pinos dos LEDs (`LED_GREEN_Pin`, `LED_GREEN_GPIO_Port`, etc.) e do botão (`BLUE_BUTTON_Pin`, `BLUE_BUTTON_GPIO_Port`) para corresponder à sua configuração de hardware.
    * Compile o código.
    * Faça o upload do código para a sua placa STM32.

## Como Usar

Após carregar o código na placa STM32:

1.  Pressione o botão azul.
2.  Os LEDs verde, amarelo e vermelho devem piscar uma vez em sequência.
3.  A cada nova pressão no botão, os LEDs piscarão novamente.

## Notas

* Este código utiliza a biblioteca Low-Layer (LL), que oferece um controle mais direto sobre o hardware. Se você estiver mais familiarizado com a HAL, as funções de controle dos GPIOs e da EXTI podem ser adaptadas para usar as funções `HAL_GPIO_Init`, `HAL_GPIO_TogglePin`, `HAL_EXTI_SetConfigLine`, etc.
* A função de callback da interrupção (`HAL_GPIO_EXTI_Callback`) está comentada no código. Em projetos que utilizam a HAL, essa função seria o ponto de entrada para o código a ser executado quando a interrupção ocorre. Neste projeto com LL, a flag é diretamente modificada dentro da rotina de tratamento da interrupção (que não está explicitamente mostrada aqui, mas é configurada via `NVIC_EnableIRQ(EXTI15_10_IRQn);`).
* Certifique-se de que as configurações de clock (`SystemClock_Config`) e GPIO (`MX_GPIO_Init`) estejam corretas para a sua placa STM32. Essas configurações podem variar dependendo do modelo específico.
* A configuração da MPU (`MPU_Config`) neste código desabilita a MPU e configura uma região de memória sem acesso. Em projetos mais complexos, a MPU é usada para proteger regiões de memória. Para este projeto simples, essa configuração específica pode não ser estritamente necessária, mas é incluída no código gerado.

## Próximos Passos

* Implementar um tempo de debounce para o botão para evitar múltiplas detecções com uma única pressão.
* Modificar o padrão de pisca dos LEDs.
* Adicionar mais funcionalidades ao projeto, como sequências de LEDs diferentes ou interação com outros periféricos.

Sinta-se à vontade para explorar e modificar este código para aprender mais sobre o controle de periféricos em microcontroladores STM32!
