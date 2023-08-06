### Bem-vindos ao meu Perfil de Trabalho 🚀🚀🚀

<div>
  <a href="https://github.com/Guilherme-DAngelo">
  <img height="180em" src="https://github-readme-stats.vercel.app/api?username=devemdobro&show_icons=true&theme=tokyonight&include_all_commits=true&count_private=true"/>
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=devemdobro&layout=compact&langs_count=6&theme=tokyonight"/>
</div>
<div style="display: inline_block"><br>
  <img align="center" alt="Js" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-plain.svg">
  <img align="center" alt="HTML" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original.svg">
  <img align="center" alt="CSS" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original.svg">
</div>
 
 <br>
 
  ### Minhas Redes Sociais Abaixo:
 
<div> 
 <a href="https://discord.com/channels/@me" target="_blank"><img src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white" target="_blank"></a> 
  <a href = "mailto:guigui.dangelo@icloud.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
  <a href="https://www.linkedin.com/in/guilherme-d-655705218/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a> 

name: generate animation

on:
 # run automatically every 24 hours
 schedule:
   - cron: "0 */24 * * *" 
 
 # allows to manually run the job at any time
 workflow_dispatch:
 
 # run on every push on the master branch
 push:
   branches:
   - master
   
 

jobs:
 generate:
   runs-on: ubuntu-latest
   timeout-minutes: 10
   
   steps:
     # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
     - name: generate github-contribution-grid-snake.svg
       uses: Platane/snk/svg-only@v3
       with:
         github_user_name: ${{ github.repository_owner }}
         outputs: |
           dist/github-contribution-grid-snake.svg
           dist/github-contribution-grid-snake-dark.svg?palette=github-dark
       env:
         GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
         
         
     # push the content of <build_dir> to a branch
     # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
     - name: push github-contribution-grid-snake.svg to the output branch
       uses: crazy-max/ghaction-github-pages@v3.1.0
       with:
         target_branch: output
         build_dir: dist
       env:
         GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
