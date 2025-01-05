
set env:
```yml
steps:
      - name: Set date variable
        id: date
        run: echo "DATE=$(date +'%y%m%d')" >> $GITHUB_ENV
# use
tag: nightly-${{ github.run_number }}-${{ env.DATE }}
```




```yml
- name: Generate tag
        id: generate_tag
        run: echo "::set-output name=tag::v$(date +'%Y%m%d-%H%M%S')".

# use it
tag: ${{ steps.generate_tag.outputs.tag }}

```

