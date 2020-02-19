# 02. Create a Single-Command Node.js CLI with Oclif, TypeScript and Yarn Workspaces

## Notes

The fastest way to create a robust, cross-platform compatible Node.js CLI is by running `npx oclif single mycli`.

Oclif is both a CLI framework and a CLI that scaffolds CLI's.

There are two ways to simulate this locally. You can actually `yarn link --global`, or you can use a yarn workspace.

## Personal Take

For local development you don't want to reinstall your CLI every time. Use symlinking.

```shell
## example 1: global dep
## in CLI folder
yarn link --global
## in project folder
myfirstcli init

## example 2: local dep
## in CLI folder
yarn link
## in project folder
yarn link myfirstcli
yarn myfirstcli init
```
