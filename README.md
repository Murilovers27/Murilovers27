# Arquivo: .github/workflows/metrics.yml
name: GitHub Metrics
on:
  # Roda todo dia à meia-noite
  schedule:
    - cron: "0 0 * * *"
  # Permite que você rode manualmente pela aba "Actions"
  workflow_dispatch:
  # Roda também quando você faz push para a branch 'main' (opcional)
  push:
    branches:
      - main
      
jobs:
  render_metrics:
    runs-on: ubuntu-latest
    steps:
      - name: Gerar Métricas
        uses: lowlighter/metrics@latest
        with:
          # (Obrigatório) Seu nome de usuário e o token do GitHub
          user: SEU-NOME-DE-USUARIO
          token: ${{ secrets.GITHUB_TOKEN }}

          # (Opcional) Quais métricas você quer?
          # Habilite tudo para este exemplo
          base: header, activity, community, repositories, metadata
          
          # (O que você pediu!) Configuração do plugin de linguagens
          plugin_languages: yes
          plugin_languages_analysis_timeout: 15
          plugin_languages_categories: markup, programming # Oculta arquivos de 'prosa'
          plugin_languages_colors: github               # Usa as cores oficiais do GitHub
          plugin_languages_limit: 8                     # Mostra as 8 linguagens mais usadas
          plugin_languages_recent_categories: markup, programming
          plugin_languages_recent_days: 14
          plugin_languages_recent_load: 300
          plugin_languages_sections: most-used, recent-activity # Mostra mais usadas E recentes
