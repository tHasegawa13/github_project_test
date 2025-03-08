# Github Project Test
業務効率化のため Github Actions を使用して Github Project や Issue の操作を行なってみる。

## workflow
- `_add_label_subissues.yaml`
  - SubIssueを切ったタイミングで、「 `subissue` 」 と 「 (親に紐づいているラベル) 」 のラベルを SubIssue にも紐づける
  - Gihtub Project に自動で紐づける
