# code-sherpas/.github

Workflows reutilizables que comparten los repositorios de Code Sherpas. Cada repositorio los llama con `uses:` y una etiqueta de versión (`@v1`); un cambio aquí sólo le llega cuando sube de etiqueta.

## Workflows

### `enqueue-dependabot-updates.yaml`

Mete en la merge queue, sin nadie de por medio, cada PR de Dependabot cuyo salto más alto es minor o patch, con el token de la GitHub App `dependabot-enqueuer` y `gh pr merge --auto`. Las major, y las PRs en las que ha hecho push una persona, siguen siendo manuales.

Adoptarlo **exime** a esas PRs de la prueba manual y de la verificación en producción (Gate 3 de `pre-merge-gates` y `post-deploy-verification`): la decide quien es responsable del repositorio. El workflow no mira las comprobaciones del repositorio; cada repositorio es responsable de las suyas.

Requisitos:

- la App `dependabot-enqueuer`, instalada en el repositorio (hoy en todos los de la organización);
- los secretos de Dependabot de la organización `DEPENDABOT_ENQUEUER_CLIENT_ID` y `DEPENDABOT_ENQUEUER_PRIVATE_KEY`, accesibles al repositorio.

La llamada, en `.github/workflows/enqueue-dependabot-updates.yaml` del repositorio, está en la cabecera del workflow.
