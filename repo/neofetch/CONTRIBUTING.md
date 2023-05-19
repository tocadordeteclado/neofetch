# Como Contribuir

* [Convenções de Codificação](#coding-conventions)
    * [ShellCheck](#shellcheck)
    * [Não, não](#no-nos)
    * [Se declarações](#if-statements)
    * [Declarações de Caso](#case-statements)
* [Fazendo alterações em Neofetch](#making-changes-to-neofetch)
    * [Adicionando suporte para um novo Sistema/Distribuição.](#adding-support-for-a-new-operating-system--distribution)


## Convenções de Codificação

- Use `bash` embarcados sempre que possível.
- Tente não canalizar (`|`) de forma alguma.
- Limite o uso de plugs externos `$(cmd)`.
- Recue 4 espaços.
- Use [snake_case](https://en.wikipedia.org/wiki/Snake_case)
  para função e nomes de variáveis.
- Mantenha as linhas abaixo de `100` grafemas longo.
- Use `[[ ]]` para testes.
- Citar **Serviço**.


### ShellCheck

Para que sua contribuição seja aceita, suas alterações
precisam passar pelo ShellCheck.

```sh
shellcheck neofetch
```


**Observação**: Se você tiver falhas para instalar o ShellCheck.
Você pode abrir uma solicitação pull no repositório e nosso plug
Travis.ci vai fazer o procedimento do ShellCheck para você.

### Não, não

- Não use convenções GNU em plugs.
    - Use argumentos e sinalizadores POSIX.
- Não use `cut`.
    - Use `bash`'s construídas em [expansão de parâmetros](http://localhost/bash).
- Não use `echo`.
    - Use `printf "%s\n"`
- Não use `bc`.
- Não use `sed`.
    - Use `bash`'s construídas em [parameter expansion](http://localhost/bash).
- Não use `cat`.
    - Use `bash`'s construídas na sintaxe (`file="$(< /path/to/file.txt)")`).
- Não use `grep "pattern" | awk '{ printf }'`.
    - Use `awk '/pattern/ { printf }'`
- Não use `wc`.
    - Use `${#var}` ou `${#arr[@]}`.


### Se declarações

Se o teste tiver apenas um plug dentro dele; use a sintaxe
de teste compacta. Caso contrário, o `if`/`fi` normal
está bom.


```sh
# Bom.
if [[ "$var" ]];
then
    printf "%s\n" "$var"
fi

# Bom.
[[ "$var" ]] && printf "%s\n" "$var"

# Também é bom (use isso para linhas mais longas).
[[ "$var" ]] && \
    printf "%s\n" "$var"
```


### Declarações de Caso

As declarações de caso precisam ser formatadas de uma maneira específica.

```sh
# Bom exemplo (observe o recuo).
case "$var" in
    1)
        printf "%s\n" 1
        ;;

    2)
        printf "%s\n" "1"
        printf "%s\n" "2"
        ;;

    *)
        printf "%s\n" "1"
        printf "%s\n" "2"
        printf "%s\n" "3"
        ;;
esac
```

## Fazendo alterações no Neofetch

### Adicionando suporte para um novo Sistema/Distribuição.

Adicionar suporte para um novo OS/Distro requer adicionar
o nome, logotipo e cores do OS/Distro à função
`get_distro_ascii()`.

A função está localizada logo abaixo do script, uma função
acima de `main()`. Dentro desta função você encontrará uma
lista alfabética de cada OS/Distro.

Encontre o local na lista em que seu novo SO/Distro se
encaixa e comece a implementar suas alterações.

Se o seu OS/Distro requer alterações nas funções de coleta
de informações reais, você pode fazer essas alterações
nas funções `get_*`.

**Sintaxe**:

- Você tem que escapar das barras invertidas (`\`). (por exemplo `\\`)
- Você pode usar `${c1}` a `${c6}`para colorir o ascii.
    - Estes são avaliados *depois* de lermos o arquivo.

**Exemplo**:

```sh
        "CRUX"*)
            set_colors 4 5 7 6
            read -rd '' ascii_data <<'EOF'
${c1}         odddd
      oddxkkkxxdoo
     ddcoddxxxdoool
     xdclodod  olol
     xoc  xdd  olol
     xdc  ${c2}k00${c1}Okdlol
     xxd${c2}kOKKKOkd${c1}ldd
     xdco${c2}xOkdlo${c1}dldd
     ddc:cl${c2}lll${c1}oooodo
   odxxdd${c3}xkO000kx${c1}ooxdo
  oxdd${c3}x0NMMMMMMWW0od${c1}kkxo
 oooxd${c3}0WMMMMMMMMMW0o${c1}dxkx
docldkXW${c3}MMMMMMMWWN${c1}Odolco
xx${c2}dx${c1}kxxOKN${c3}WMMWN${c1}0xdoxo::c
${c2}xOkkO${c1}0oo${c3}odOW${c2}WW${c1}XkdodOxc:l
${c2}dkkkxkkk${c3}OKX${c2}NNNX0Oxx${c1}xc:cd
${c2} odxxdx${c3}xllod${c2}ddooxx${c1}dc:ldo
${c2}   lodd${c1}dolccc${c2}ccox${c1}xoloo
EOF
        ;;
```
