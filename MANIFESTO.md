> **Como usar:** Abra o Claude Code na raiz do projeto clonado e cole o prompt abaixo seguido do conteúdo deste arquivo.

**Prompt para o Claude Code:**
```
Você está implementando o site do cliente Paulo Alexandre Souza Pires (segmento: Direito de Trânsito / Recursos Administrativos).
Leia este documento do início ao fim antes de começar. Depois siga passo a passo:

1. Preencha `src/styles/tokens.css` com as cores da seção "Direção de Arte" (apenas os valores — os nomes são fixos)
2. Atualize o `<link>` de fonte serifada no `BaseLayout.astro` conforme a tipografia indicada
3. Preencha `src/pages/index.astro` com imports dos componentes e ordem das seções
4. Para cada seção, substitua os textos placeholder pela copy indicada neste documento
5. Preencha `.env` com WhatsApp, GTM e domínio — o template já lê essas variáveis
6. Preencha o `defaultSchema` no `BaseLayout.astro` com os dados do Schema.org
7. Preencha os TODOs em `politica-de-privacidade.astro` e `termos-de-uso.astro` com dados reais
8. Garanta: Hero com `id="hero-section"`, Footer com `id="footer"`, main com `id="main-content"`
9. Rode `npm run build` para validar — corrija qualquer erro antes de considerar pronto

Regras absolutas:
- NUNCA hardcode cor, fonte ou tamanho — sempre `var(--t-*)` ou classes utilitárias Tailwind
- `<Image />` do Astro, nunca `<img>` nativo
- Sem `any` no TypeScript, sem `!important` no CSS
- Tema padrão: claro (padrão)
```

---

# Documento do Projeto — Paulo Alexandre Souza Pires
**Studio:** Astroteca Studio
**Gerado em:** 08/06/2026
**Segmento:** Direito de Trânsito / Recursos Administrativos
**Tipo:** servico

---

## Briefing do Cliente

| Campo | Valor |
|-------|-------|
| Nome do cliente | Paulo Alexandre Souza Pires |
| Nome da marca | CANCELA MULTAS |
| Segmento | Direito de Trânsito / Recursos Administrativos |
| Tipo de negócio | servico |
| Proposta de valor | Somos uma empresa especializada em recursos de multas e defesa de trânsito, focada em proteger a CNH dos nossos clientes com agilidade, transparência e estratégia. Ajudamos motoristas a evitar prejuízos financeiros, suspensão da carteira e complicações burocráticas, oferecendo atendimento especializado e soluções personalizadas para cada situação. |
| Domínio | cancelamulta.com.br |
| WhatsApp | 5548996729999 |
| Horários | segunda a sábado |
| Objetivo de conversão | Contato via WhatsApp para análise de multa ou contratação de serviço |
| Mensagem WhatsApp | Olá! Vim do Google e gostaria de mais informações |
| GTM ID |  GTM-M7S2PDFR |
| Schema tipo | LocalBusiness |
| Serviço principal | Recursos Administrativos de Multas de Trânsito |
| Público primário | Motoristas com multas de trânsito, condutores com CNH em risco de suspensão ou cassação, motoristas profissionais (aplicativo, caminhoneiros) que dependem da CNH para trabalhar. |
| Dor do público | Perda da CNH, muitos pontos, multa alta, impacto profissional, prejuízos financeiros, suspensão da carteira, complicações burocráticas e estresse com processos de trânsito. |
| Resultado esperado | Maior chance de cancelar ou reduzir penalidades de multas, proteção da CNH, economia de dinheiro, redução de estresse e burocracia, e mais segurança para continuar dirigindo e trabalhando. |
| Frase de impacto | Defendemos sua CNH, reduzimos prejuízos e transformamos multas em soluções rápidas e inteligentes — com atendimento ágil, análise especializada e máxima chance de sucesso no seu recurso. |
| Diferencial | Unimos tecnologia, agilidade e atendimento especializado para proteger sua CNH com transparência, estratégia e máxima eficiência. |
| SEO título | Cancela Multas | Recursos de Trânsito e Defesa da CNH Online |
| SEO descrição | Especialistas em recursos de multas de trânsito e defesa da CNH em todo o Brasil. Proteja sua carteira contra suspensão e cassação com agilidade, transparência e análise técnica detalhada. Análise inicial gratuita! |
| SEO keywords | recurso multa, cancelar multa, defesa CNH, lei seca, suspensão CNH, cassação CNH, direito de trânsito, multa de trânsito, processo administrativo multa |

### FAQ

1. “Toda multa pode ser cancelada?” Não. Cada caso precisa ser analisado individualmente. Existem multas com maiores chances de sucesso devido a erros técnicos, falhas no auto de infração ou problemas no processo administrativo. 2. “Vale a pena recorrer de multa?” Sim, principalmente quando há risco de: perda da CNH, muitos pontos, multa alta, impacto profissional para quem dirige diariamente. O recurso pode evitar prejuízos financeiros e administrativos. 3. “Quanto tempo demora um recurso?” O prazo varia conforme o órgão responsável e a etapa do processo. Em média, pode levar de algumas semanas a alguns meses. 4. “Posso continuar dirigindo enquanto o processo está em andamento?” Na maioria dos casos, sim. Enquanto houver possibilidade de defesa e o processo estiver em andamento, o motorista normalmente mantém o direito de dirigir. 5. “Vocês garantem vitória no recurso?” Não trabalhamos com promessas irreais. Fazemos uma análise técnica completa e buscamos a melhor estratégia possível para aumentar as chances de sucesso. 6. “Preciso ir até o escritório?” Não necessariamente. Grande parte do atendimento e envio de documentos pode ser feita totalmente online pelo WhatsApp ou e-mail. 7. “Quais documentos são necessários?” Normalmente: CNH, documento do veículo, notificação da multa, e informações do caso. Nossa equipe orienta tudo passo a passo. 8. “Vocês atendem apenas multas comuns?” Não. Também atuamos em: suspensão da CNH, cassação, Lei Seca, excesso de pontos, defesa administrativa de trânsito. 9. “Quanto custa um recurso?” O valor depende do tipo de processo, complexidade e etapa da defesa. Após a análise inicial, apresentamos um orçamento transparente. 10. “Se eu perder o recurso, o que acontece?” O cliente recebe toda orientação sobre os próximos passos possíveis, incluindo novas etapas administrativas quando cabíveis. 11. “Motorista de aplicativo ou caminhoneiro tem mais chance de precisar desse serviço?” Sim. Profissionais que dependem da CNH para trabalhar costumam procurar o serviço com frequência devido ao alto volume de circulação e risco de pontuação. 12. “Como sei se minha CNH corre risco de suspensão?” Nossa equipe faz uma análise da pontuação, histórico e tipo de infração para verificar a situação da carteira e orientar a melhor solução.

### Objeções a Quebrar

Dúvidas sobre a possibilidade de cancelamento de multas, a validade de recorrer, tempo de processo, continuidade do direito de dirigir, garantia de vitória, necessidade de atendimento presencial, documentos necessários, abrangência dos serviços e custos.

### Planos e Preços

**Infrações médias:** R$40,00


**Infrações graves:** R$80,00



---

## Estrutura da Página

### 1. Header

| Campo | Texto |
|-------|-------|
| logoAlt | CANCELA MULTAS |
| ctaTexto | Falar no WhatsApp |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |
| logo | CANCELA MULTAS |
| horrio | Atendimento: Seg a Sáb |

### 2. Hero

| Campo | Texto |
|-------|-------|
| titulo | Levou Multa ou sua CNH Pode ser Suspensa? A Gente Resolve. |
| subtitulo | Somos especialistas em recursos administrativos de trânsito. Analisamos seu caso gratuitamente e aplicamos a estratégia certa para proteger sua carteira de motorista. Atendimento 100% online em todo o Brasil. |
| ctaTexto | Analisar Minha Multa Agora |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |
| ctaSecundarioTexto | Falar com um Especialista |
| badge | Análise Inicial Gratuita |
| servico1Titulo | Atendimento rápido pelo WhatsApp, sem burocracia |
| servico2Titulo | Recurso para multas médias, graves, gravíssimas e processos suspensivos |
| servico3Titulo | Análise gratuita antes de qualquer pagamento |

### 3. Serviços

| Campo | Texto |
|-------|-------|
| titulo | Qual é a Sua Situação? |
| subtitulo | Atendemos desde multas comuns até processos de suspensão e cassação da CNH. Veja qual serviço se encaixa no seu caso. |
| servico1Titulo | Recurso de infrações médias, graves ou gravíssimas sem efeito suspensivo |
| servico2Titulo | Recurso de infrações com efeito suspensivo |
| servico3Titulo | PSDD – Processo de Suspensão do Direito de Dirigir e PCDD – Processo de Cassação do Direito de Dirigir |
| servio_1_nome | Recurso sem Efeito Suspensivo |
| servio_1_descrio | Para infrações médias, graves e gravíssimas que ainda não afetam sua CNH imediatamente. Analisamos a multa, identificamos erros técnicos e entramos com o recurso mais adequado para reduzir ou cancelar a penalidade. |
| servio_1_preos | Médias: R$40 | Graves: R$80 | Gravíssimas: R$120 |
| servio_1_cta | Quero Recorrer desta Multa |
| servio_2_nome | Recurso com Efeito Suspensivo |
| servio_2_descrio | Alguns tipos de infração suspendem a CNH assim que são aplicadas. Se você recebeu uma multa gravíssima com efeito suspensivo, precisa agir rápido. Analisamos seu caso e buscamos reverter a suspensão antes que ela entre em vigor. |
| servio_2_cta | Analisar Minha Situação Agora |
| servio_3_nome | Suspensão e Cassação da CNH (PSDD e PCDD) |
| servio_3_descrio | Se você acumulou pontos demais ou está respondendo a um processo de suspensão ou cassação, ainda há como se defender. Montamos a estratégia adequada para cada etapa e acompanhamos até a decisão final. |
| servio_3_cta | Quero Defender Minha CNH |
| servio_4_nome | Outros Processos de Trânsito |
| servio_4_descrio | Atuamos também em multas na CNH provisória, casos de Lei Seca, ação de indicação de condutor e outros processos administrativos de trânsito. Fale com a gente para analisar o seu caso específico. |
| servio_4_cta | Falar sobre Meu Caso |

### 4. Diferenciais

| Campo | Texto |
|-------|-------|
| titulo | Por que Confiar na Cancela Multas? |
| subtitulo | Não somos um escritório genérico. Somos especialistas em trânsito com foco em resultado real e transparência total em cada caso. |
| diferencial1 | Atendimento rápido e humanizado pelo WhatsApp |
| diferencial2 | Análise técnica detalhada de cada multa antes do recurso |
| diferencial3 | Transparência total sobre chances reais de sucesso |
| diferencial_1_ttulo | Análise Técnica Detalhada Antes do Recurso |
| diferencial_1_descrio | Estudamos cada detalhe da sua multa antes de qualquer ação: erros técnicos, falhas no auto de infração e argumentos que aumentam as chances de sucesso. |
| diferencial_2_ttulo | Transparência Total sobre as Chances Reais |
| diferencial_2_descrio | Você sabe exatamente o que pode esperar antes de pagar qualquer coisa. Sem promessas que não podemos cumprir e sem surpresas no meio do processo. |
| diferencial_3_ttulo | Especialistas em Suspensão, Cassação e Lei Seca |
| diferencial_3_descrio | Além dos recursos comuns, atuamos em casos graves que exigem conhecimento específico e resposta rápida. São situações em que a escolha do especialista faz toda a diferença. |
| diferencial_4_ttulo | Acompanhamento Completo até a Decisão Final |
| diferencial_4_descrio | Cuidamos de prazos, documentos e todas as etapas do processo. Você não fica sem resposta e não precisa correr atrás de nada sozinho. |
| diferencial_5_ttulo | Linguagem Simples, sem Juridiquês |
| diferencial_5_descrio | Explicamos tudo de forma clara e direta. Você entende o que está acontecendo no seu caso sem precisar decifrar termos técnicos. |
| diferencial_6_ttulo | Atendimento Online em Todo o Brasil |
| diferencial_6_descrio | Motoristas de qualquer estado são atendidos pelo WhatsApp. Toda a documentação é processada de forma digital, com segurança e agilidade. |

### 5. Preços

| Campo | Texto |
|-------|-------|
| titulo | Quanto Custa Recorrer da Sua Multa? |
| subtitulo | Valores diretos para os tipos de recurso mais comuns. Para suspensão, cassação e outros casos específicos, a análise inicial é gratuita e o orçamento é apresentado antes de qualquer compromisso. |
| ctaTexto | Solicitar Análise Gratuita |
| badge | Análise Inicial Gratuita |
| plano_1_nome | Infração Média |
| plano_1_preo | R$40,00 |
| plano_1_descrio | Recurso administrativo para infrações de natureza média |
| plano_1_cta | Quero Recorrer |
| plano_2_nome | Infração Grave |
| plano_2_preo | R$80,00 |
| plano_2_descrio | Recurso administrativo para infrações de natureza grave |
| plano_2_destaque | Mais Solicitado |
| plano_2_cta | Quero Recorrer |
| plano_3_nome | Infração Gravíssima |
| plano_3_preo | R$120,00 |
| plano_3_descrio | Recurso administrativo para infrações gravíssimas sem efeito suspensivo |
| plano_3_cta | Quero Recorrer |
| nota | Processos com efeito suspensivo, suspensão (PSDD), cassação (PCDD) e outros casos específicos são orçados individualmente após análise gratuita. Nenhuma surpresa, sempre transparência. |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |

### 6. FAQ

| Campo | Texto |
|-------|-------|
| titulo | Perguntas Frequentes |
| subtitulo | Respondemos as dúvidas mais comuns antes que você precise perguntar. |
| pergunta_1 | Toda multa pode ser cancelada? |
| resposta_1 | Não. Cada caso é analisado individualmente. Existem multas com chances maiores de sucesso devido a erros técnicos, falhas no auto de infração ou problemas no processo administrativo. Por isso fazemos uma análise técnica antes de qualquer recurso. |
| pergunta_2 | Vale a pena recorrer da multa? |
| resposta_2 | Sim, principalmente quando há risco de perda da CNH, pontos acumulados, multa de valor alto ou impacto direto na sua renda. O recurso pode evitar prejuízos financeiros e administrativos significativos. |
| pergunta_3 | Vocês garantem vitória no recurso? |
| resposta_3 | Não trabalhamos com promessas irreais. Fazemos uma análise técnica completa e aplicamos a melhor estratégia disponível para aumentar as chances de sucesso. O resultado final depende dos órgãos competentes. |
| pergunta_4 | Preciso ir até um escritório? |
| resposta_4 | Não. Todo o atendimento e envio de documentos é feito online pelo WhatsApp ou e-mail. Atendemos motoristas de qualquer estado sem que você precise sair de casa. |
| pergunta_5 | Posso continuar dirigindo durante o processo? |
| resposta_5 | Na maioria dos casos, sim. Enquanto houver possibilidade de defesa e o processo estiver em andamento, o motorista normalmente mantém o direito de dirigir. Verificamos isso já na análise inicial. |
| pergunta_6 | Quanto tempo demora um recurso? |
| resposta_6 | O prazo varia conforme o órgão responsável e a etapa do processo. Em média, pode levar de algumas semanas a alguns meses. Você é informado sobre o andamento em cada etapa. |
| ctaTexto | Tirar Minha Dúvida Agora |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |

### 7. CTA Final

| Campo | Texto |
|-------|-------|
| titulo | Não Deixe sua CNH em Risco. Fale com a Gente Agora. |
| subtitulo | Envie sua multa pelo WhatsApp e receba uma análise gratuita com orientação sobre as reais chances do seu recurso. Sem compromisso. |
| ctaTexto | Analisar Minha Multa Grátis |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |
| badge | Análise Gratuita |
| horrio | Atendimento de Segunda a Sábado |

### 8. Footer

| Campo | Texto |
|-------|-------|
| copyright | © 2026 Cancela Multas. Todos os direitos reservados. |
| politicaUrl | /politica-de-privacidade |
| marca | CANCELA MULTAS |
| cta_whatsapp | Falar no WhatsApp |
| ctaUrl | https://wa.me/5548996729999?text=Ol%C3%A1!%20Vim%20do%20Google%20e%20gostaria%20de%20mais%20informa%C3%A7%C3%B5es |
| telefone | +55 48 99672-9999 |
| atendimento | Segunda a Sábado |
| site | cancelamulta.com.br |
| aviso_legal | Os serviços prestados possuem natureza administrativa e consultiva. Cada processo é analisado individualmente, não havendo garantia de deferimento ou cancelamento de multas, pois as decisões dependem exclusivamente dos órgãos competentes. |
| poltica_de_transparncia | Trabalhamos com análise técnica, atendimento ético e orientação clara sobre as reais possibilidades de cada caso. |
| privacidade_e_segurana | Todos os dados e documentos enviados pelos clientes são tratados com sigilo e segurança, conforme a legislação vigente. |
| atendimento_nacional | Atendimento online e suporte especializado em todo o Brasil. |



---

## Direção de Arte

### Tema Padrão
**Claro**

### Cores — `src/styles/tokens.css`

Preencha **apenas os valores** (os nomes são fixos entre projetos):

```css
:root {
  --t-primary:      #144e74;
  --t-primary-dark: #0f3e5e;
  --t-secondary:    #edbd24;
  --t-background:   #fcfcfc;
  --t-surface:      #fafafa;
  --t-surface-alt:  #f0f4f7;
  --t-dark:         #1a1a1a;
  --t-text-main:    #333333;
  --t-text-soft:    #595959;
  --t-text-muted:   #808080;
  --t-border:       #d8d8d8;
}

.dark {
  --t-background:  #121212;
  --t-surface:     #212121;
  --t-surface-alt: #303030;
  --t-text-main:   #e6e6e6;
  --t-text-soft:   #b3b3b3;
  --t-text-muted:  #737373;
  --t-border:      #333333;
}
```

### Tipografia

| Papel | Fonte |
|-------|-------|
| Heading (`font-serif`) | Inter |
| Body (`font-sans`) | Inter |

### Mood & Referências

Um visual moderno e sofisticado que inspira confiança e profissionalismo, utilizando uma paleta de cores sóbrias com toques vibrantes para representar a agilidade e a inteligência tecnológica das soluções.

**Referências visuais:** https://www.resolvmultas.com.br/
https://reavermultas.com.br/
https://www.somultas.com/

**Notas:** A qualidade da referencia https://www.somultas.com/ é muito boa devemos conseguir algo semelhante ou até melhor, mas precisamos de ser originais e autentico

---

## Regras de Copy — DNA do Negócio

## DNA: Prestador de Serviço

**Tom:** Confiante, direto, focado em resultado tangível.
**Perspectiva:** "Eu resolvo seu problema" — não "eu ofereço um serviço".
**Foco:** Transformação antes/depois. O visitante deve sentir que o problema dele tem solução aqui.

**Copy que funciona:**
- Hero: atacar a dor principal no título. Subheadline com o resultado esperado.
- CTA: verbos de ação imediata — "Agende agora", "Fale comigo hoje", "Quero resolver isso".
- Sobre: credenciais rapidamente, depois voltar ao cliente — não fazer monólogo sobre si.
- Depoimentos: resultado específico + prazo + nome real. Ex: "Resolvi em 3 dias o que levava semanas".

**Evitar:** Jargão técnico, parágrafos longos, muito sobre o processo e pouco sobre o resultado.

---

## Checklist Final

- [ ] `npm run build` sem erros de TypeScript/Astro
- [ ] `src/styles/tokens.css` preenchido com cores reais do cliente
- [ ] Fontes carregadas: `<link>` no `BaseLayout.astro` + import `@fontsource` no `global.css`
- [ ] `.env` preenchido: `PUBLIC_WA_NUMBER`, `PUBLIC_WA_MESSAGE`, `PUBLIC_GTM_ID`, `PUBLIC_SITE_URL`
- [ ] `BaseLayout.astro`: title, description, OG, canonical, Schema.org JSON-LD
- [ ] Hero com `id="hero-section"`; Footer com `id="footer"`; main com `id="main-content"`
- [ ] Header: esconde ao rolar para baixo; link ativo por IntersectionObserver
- [ ] WhatsApp flutuante: some quando Hero ou Footer estão visíveis; número real no `.env`
- [ ] Dark mode: toggle no Footer; persiste localStorage; sem flash na primeira carga
- [ ] Todas as seções com copy real (sem placeholder genérico)
- [ ] Responsivo em mobile (375px): texto ≥ 20px, botões ≥ 44px, padding lateral ≥ 20px
- [ ] `politica-de-privacidade.astro` e `termos-de-uso.astro`: TODOs preenchidos
- [ ] Schema tipo: `LocalBusiness`
- [ ] GTM configurado (ID:  GTM-M7S2PDFR)
- [ ] WhatsApp (número: 5548996729999)