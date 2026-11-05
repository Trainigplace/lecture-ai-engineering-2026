# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：巣のLLMでは、説明が長く、もっともらしい回答をしているが、正確に答えていない。一方、エージェントはGlossaryの回答を正確に参照しており、言葉遣いが異なるだけである。
- `--trace` で見えたツール呼び出し（ツール名と引数）：[tool call]   search_glossary({'query': 'LoRA'})
[tool call]   search_glossary({'query': 'QLoRA'})

[usage] RunUsage(cost=Decimal('0.0008738'), details={'text_prompt_tokens': 1196}, input_text_tokens=1196, input_tokens=1196, output_tokens=206, requests=2, tool_calls=2)

- 1つの質問での LLM 呼び出し回数（`requests`）：　requests=2
- 追加したツールと、docstring に書いた説明： 
ツール：make_quiz 
docstringに書いた説明："""指定した回の用語から1つを選び、確認問題と答えを返す。「第2回の確認問題を出して」のように、復習用の問題を求められたときに使う。
"""

## 宿題

- 取り組んだレベル：基礎
- やったこと：　agent.pyのInstructionから「必ず search_glossary で用語集を確認する」の行を消すと、検索せずに答えるようになるか　を検証した。
- 結果：該当の行を削除しても、検索は省略されていなかった。
- 気づき・疑問：
ツール定義（description）が呼び出しを誘導している：ツールの説明文や他の指示（「講座の用語集に基づく」など）が残っていれば、明示の行がなくても呼ぶ可能性がある。そのため、回数を重ねると参照しない回答があるかもしれない。
質問が用語集の語そのもの：「LoRAとQLoRA」は用語集の見出し語と一致するため、モデルが「検索すべき質問」と判断しやすい題材だったかもしれない。

