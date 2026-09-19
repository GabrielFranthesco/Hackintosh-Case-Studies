# 🖥️ Hackintosh Case Studies & Infrastructure Lab

Repositório dedicado ao estudo prático de arquitetura de computadores, compatibilidade de hardware e engenharia de sistemas através de tentativas de instalação do macOS em hardware não oficial (PC x86).

Este espaço demonstra tanto a implementação bem-sucedida de um ecossistema quanto a análise crítica de falhas e gestão de riscos em cenários de infraestrutura.

---

## 🚀 Setup 01: O Setup Principal (Caso de Sucesso)

Configuração principal totalmente funcional, focada em estabilidade, otimização e validação de desempenho de componentes modernos.

### 🛠️ Hardware do Sistema
* **Processador:** AMD Ryzen 5 4600G
* **Memória RAM:** 16GB DDR4
* **Placa de Vídeo (GPU):** AMD Radeon RX 6650XT
* **Bootloader:** OpenCore

### ✨ Status de Funcionamento
* [x] Aceleração gráfica nativa (RX 6650XT)
* [x] Gerenciamento de energia e estados C/P
* [x] Portas USB mapeadas e funcionais
* [x] Áudio onboard

> 📂 *A pasta `EFI` otimizada para este hardware encontra-se disponível neste repositório para fins de estudo e referência.*

---

## ⚠️ Setup 02: O Setup Secundário & Post-Mortem (Lição Aprendida)

Tentativa de implementação em um ambiente de hardware alternativo/reaproveitado, culminando em um cenário de falha controlada e encerramento estratégico do projeto.

### 🛠️ Hardware do Sistema
* **Processador:** Intel Xeon E5-2680v4
* **Memória RAM:** 32GB ECC/DRAM
* **Placa de Vídeo (GPU):** AMD Radeon RX 580 2048SP (Versão modificada para mineração)

### 🔍 O Problema, Diagnóstico e Análise Técnica
1. **O Bloqueio Inicial (Legacy vs. UEFI):** O bootloader OpenCore e o ecossistema do macOS exigem obrigatoriamente o modo UEFI. No modo *Legacy*, a instalação sequer iniciava. Porém, ao alterar a placa-mãe para o modo UEFI, o sistema perdia totalmente o sinal de vídeo na inicialização, exigindo um *reset* físico da BIOS.
2. **A Raiz do Problema (VBIOS Modificada):** Constatou-se que a RX 580 2048SP operava com uma VBIOS modificada — comum em placas vindas de mineração —, que não era compatível com o padrão UEFI necessário para a placa-mãe reconhecer o vídeo corretamente.
3. **O Incidente e Mitigação:** A tentativa de atualizar a VBIOS para resolver essa incompatibilidade acabou corrompendo a placa (*brick* parcial) e deixando o Setup 02 sem vídeo. O prejuízo total foi evitado graças à precaução de ter feito um **backup prévio da firmware**, o que permitiu recuperar a placa.
4. **A Decisão de Engenharia (Trade-off):** Como o processador Xeon do Setup 02 não possui vídeo integrado, cada ciclo de recuperação exigia desconectar a placa corrompida, levá-la até o **Setup 01** (computador com Ryzen e vídeo integrado) para conseguir dar vídeo e regravar o backup, e depois devolvê-la ao Setup 02. Devido a esse alto atrito operacional e ao risco contínuo para o hardware, optou-se pelo encerramento consciente do projeto.
