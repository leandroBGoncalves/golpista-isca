golpista-isca 🛡️

Ferramenta de dissuasão contra golpistas que tentam clonar WhatsApp via engenharia social em plataformas de classificados (ex.: OLX).

Este projeto disponibiliza uma página isca que você pode enviar a um contato suspeito (golpista). A página simula uma "validação de código" mas, ao ser acessada, exibe um aviso intimidador de monitoramento antifraude, registra informações básicas de acesso (IP, user-agent, horário) e aplica alguns efeitos visuais para parecer que o dispositivo está sendo analisado.

⚖️ Uso responsável: Este projeto não executa código malicioso, não invade dispositivos e não coleta dados sensíveis além do que o navegador fornece voluntariamente (IP, user-agent etc.). É uma ferramenta educacional e dissuasiva.

✨ Recursos

Interface de alerta com visual "cibercrime / rastreamento".

Mensagem intimidadora citando Coordenação de Repressão a Crimes Cibernéticos (Cibercrime).

Coleta passiva de:

IP de acesso (incluindo cabeçalho x-forwarded-for quando disponível).

User-Agent (pode indicar sistema operacional / navegador).

Data e hora (ISO8601).

Consulta opcional de geolocalização aproximada via IPInfo.io.

Tela de análise simulada que bloqueia cliques por ~15s.

Ocultação de cursor e rolagem (efeito de travamento).

Tentativa de fullscreen discreta no primeiro toque (limitada pelas políticas do navegador).

Registro de acessos em logs.txt no servidor.

🚨 Quando usar

Use quando você suspeitar que um contato está tentando aplicar o golpe do "código de verificação enviado por SMS" para clonar seu WhatsApp. Em vez de discutir, envie um link da página isca. Quando o golpista abrir:

Ele verá uma tela de "validação" / "análise".

O sistema exibirá aviso de monitoramento antifraude.

Seu acesso será logado para futura denúncia.

📁 Estrutura do projeto

golpista-isca/
├── public/
│   └── index.html        # Página isca (UI, alerta, fullscreen, IPInfo)
├── server.js             # Servidor Express + logging
├── package.json          # Dependências Node
└── logs.txt              # (criado em runtime) Registro de acessos

⚙️ Instalação local

Requer Node.js >= 18.

git clone https://github.com/SEU_USUARIO/golpista-isca.git
cd golpista-isca
npm install express
node server.js

Abra: http://localhost:3000

🔐 Configurar token do IPInfo (geolocalização)

Crie uma conta gratuita: https://ipinfo.io/signup

Copie seu Token de Acesso.

Edite public/index.html e substitua:

fetch("https://ipinfo.io/json?token=SEU_TOKEN_AQUI")

por:

fetch("https://ipinfo.io/json?token=SEU_TOKEN_REAL")

Salve e reinicie o servidor.

Se não configurar o token, a localização poderá aparecer vazia.

🖥️ Deploy

Você pode publicar a página em qualquer host Node. Abaixo, duas rotas recomendadas.

Opção A — Render.com (recomendada: logs funcionando)

Suba o projeto para um repositório GitHub privado ou público.

Crie conta em https://render.com.

New + Web Service → conecte seu repositório.

Configurações:

Runtime: Node

Build Command: npm install

Start Command: node server.js

Deploy. Seu app sairá algo como:
https://codigo-verificacao.onrender.com

Os logs serão gravados em arquivo efêmero. Para persistência longa, use volumes, um bucket ou logging externo.

Opção B — Vercel (estático / sem logs de arquivo)

O Vercel funciona melhor para projetos estáticos. Como usamos Express + fs, você teria que:

Migrar o log para uma Serverless Function (Edge / Node).

Armazenar dados em serviço externo (por ex.: Inngest, Upstash Redis, Supabase).

Se quiser essa versão serverless, abra uma issue (ver seção abaixo) que disponibilizo um exemplo.

🧪 Fluxo de uso sugerido

Publica anúncio de celular (OLX, grupos etc.) com número alternativo ou chat interno.

Se alguém pedir "o código de verificação da OLX" → suspeite.

Responda: "Acabei de receber aqui, veja se confere: https://SEU-LINK".

Golpista clica → você registra o acesso.

Use logs.txt + prints da conversa para denúncia.

📝 Exemplo de resposta pronta para enviar ao suspeito

"Opa, caiu aqui um código, confere nesse link oficial de validação: https://SEU-LINK. Se não abrir me avisa."

Versão mais ríspida:

"Validação OLX automática: https://SEU-LINK. Se der erro me chama."

📄 Formato dos logs

Cada acesso gera uma linha:

[2025-07-20T15:22:11.123Z] IP: 203.0.113.42 | User-Agent: Mozilla/5.0 (Linux; Android 12; SM-A125M) Chrome/126.0

Dica: importar logs.txt no Excel / Sheets usando separador | para analisar padrões.

🧰 Extensões e melhorias sugeridas



Abra uma issue ou PR se quiser contribuir.

🛡️ Aviso legal (detalhado)

Este projeto é disponibilizado "como está", sem garantias. Ao usar:

Você concorda em utilizá-lo apenas para fins educativos, de conscientização ou autoproteção.

Não utilize esta ferramenta para enganar, chantagear, atacar ou retaliar qualquer pessoa.

Não tente modificar o código para executar ações invasivas, coleta de dados sigilosos ou acesso não autorizado a dispositivos ou contas.

A responsabilidade pelo uso é inteiramente do usuário.

🌐 Versão em inglês (resumo)

golpista-isca is a decoy page to deter WhatsApp social-engineering scammers. It collects passive access data (IP, user-agent), shows a strong anti-fraud alert UI, simulates a device scan, and helps victims document scam attempts for reporting to authorities. Educational use only. No malware. No device exploitation.

🤝 Contribuindo

Pull requests são bem-vindos! Para grandes mudanças:

Abra uma issue descrevendo o que quer alterar.

Explique o caso de uso.

Teste antes de enviar.

📜 Licença

Sugestão: MIT License (ou escolha outra). Exemplo curto:

Este software é distribuído sob a licença MIT. Consulte LICENSE para detalhes.

📫 Contato

Se quiser suporte ou versão com backend externo (Sheets, DB, Telegram alertas), crie uma issue ou entre em contato.

Fique seguro. Não compartilhe códigos de verificação com ninguém.