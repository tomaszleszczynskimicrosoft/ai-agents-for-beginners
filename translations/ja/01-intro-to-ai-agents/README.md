# AIエージェントとそのユースケース入門

「初心者向けAIエージェント」コースへようこそ！このコースでは、AIエージェントを構築するための基本的な知識と実践的なサンプルを学べます。

[Azure AI Discord Community](https://discord.gg/kzRShWzttr) に参加して、他の学習者やAIエージェント開発者と交流し、このコースに関する質問を自由にしてください。

このコースを始めるにあたり、まずAIエージェントとは何か、そしてそれを私たちのアプリケーションやワークフローでどのように活用できるかを理解するところから始めます。

## はじめに

このレッスンでは以下を学びます：

- AIエージェントとは何か、そしてその種類にはどのようなものがあるのか？
- AIエージェントが適しているユースケースとは？また、それがどのように役立つのか？
- エージェントソリューションを設計する際の基本的な構成要素は何か？

## 学習目標
このレッスンを修了すると、以下ができるようになります：

- AIエージェントの概念を理解し、他のAIソリューションとの違いを把握する。
- AIエージェントを最も効率的に活用する。
- ユーザーと顧客の両方にとって生産的なエージェントソリューションを設計する。

## AIエージェントの定義と種類

### AIエージェントとは？

AIエージェントは、**大規模言語モデル（LLM）** に **ツールや知識へのアクセス** を提供し、その能力を拡張することで **アクションを実行** できるようにする **システム** です。

この定義を分解してみましょう：

- **システム** - エージェントを単一のコンポーネントとしてではなく、複数のコンポーネントから成るシステムとして考えることが重要です。AIエージェントの基本的な構成要素は以下の通りです：
  - **環境** - AIエージェントが動作する定義された空間。例えば、旅行予約のAIエージェントの場合、環境はエージェントがタスクを完了するために使用する旅行予約システムとなります。
  - **センサー** - 環境には情報があり、フィードバックを提供します。AIエージェントはセンサーを使用して、環境の現在の状態に関する情報を収集・解釈します。旅行予約エージェントの例では、ホテルの空室状況や航空券の価格などの情報を旅行予約システムから取得します。
  - **アクチュエーター** - AIエージェントが環境の現在の状態を受け取った後、そのタスクに応じて環境を変化させるためにどのようなアクションを実行するかを決定します。旅行予約エージェントの場合、ユーザーのために空室を予約するアクションが該当します。

![What Are AI Agents?](../../../translated_images/what-are-ai-agents.125520f55950b252a429b04a9f41e0152d4dafa1f1bd9081f4f574631acb759e.ja.png?WT.mc_id=academic-105485-koreyst)

**大規模言語モデル** - エージェントの概念自体はLLMが誕生する以前から存在していましたが、LLMを用いたAIエージェント構築の利点は、人間の言語やデータを解釈する能力にあります。この能力により、LLMは環境情報を解釈し、環境を変化させるための計画を立てることができます。

**アクションの実行** - AIエージェントシステムの外では、LLMはユーザーのプロンプトに基づいてコンテンツや情報を生成する状況に限定されます。一方で、AIエージェントシステム内では、LLMはユーザーのリクエストを解釈し、環境内で利用可能なツールを使用することでタスクを達成することができます。

**ツールへのアクセス** - LLMがアクセスできるツールは、1) その動作環境と、2) AIエージェントの開発者によって定義されます。旅行エージェントの例では、エージェントのツールは予約システムで利用可能な操作によって制限される場合や、開発者がフライト予約に限定する場合があります。

**知識** - 環境から提供される情報以外にも、AIエージェントは他のシステム、サービス、ツール、さらには他のエージェントから知識を取得することができます。旅行エージェントの例では、顧客データベースに保存されたユーザーの旅行の好みに関する情報が該当します。

### AIエージェントの種類

AIエージェントの一般的な定義を理解したところで、特定のエージェントタイプと、それらが旅行予約AIエージェントにどのように適用されるかを見てみましょう。

| **エージェントタイプ**         | **説明**                                                                                                                        | **例**                                                                                                                                                                                                                     |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **単純反射エージェント**       | 定義されたルールに基づいて即座にアクションを実行します。                                                                            | 旅行エージェントがメールの文脈を解釈し、旅行の苦情をカスタマーサービスに転送します。                                                                                                                                        |
| **モデルベース反射エージェント** | 世界のモデルとその変化に基づいてアクションを実行します。                                                                             | 旅行エージェントが過去の価格データへのアクセスを基に、大幅な価格変動があるルートを優先します。                                                                                                                        |
| **目標ベースエージェント**      | 目標を解釈し、それを達成するためのアクションを決定して計画を立てます。                                                               | 旅行エージェントが現在地から目的地までの移動手段（車、公共交通機関、フライト）を決定し、旅行を予約します。                                                                                                               |
| **効用ベースエージェント**      | 好みを考慮し、数値的にトレードオフを比較して目標を達成する方法を決定します。                                                           | 旅行エージェントが利便性とコストを比較して最大効用を得るように旅行を予約します。                                                                                                                                        |
| **学習エージェント**           | フィードバックに応じて行動を調整し、時間とともに改善します。                                                                         | 旅行エージェントが旅行後のアンケートから顧客のフィードバックを利用し、将来の予約を調整して改善します。                                                                                                                  |
| **階層型エージェント**         | 複数のエージェントが階層的に構成され、高次のエージェントがタスクをサブタスクに分割し、下位エージェントがそれを完了します。                                             | 旅行エージェントが旅行をキャンセルする際、タスクを（例えば、特定の予約のキャンセルなど）サブタスクに分割し、下位エージェントがそれを完了し、高次エージェントに報告します。                                                        |
| **マルチエージェントシステム(MAS)** | 協力的または競争的に、エージェントが独立してタスクを完了します。                                                                     | 協力的: 複数のエージェントがホテル、フライト、エンターテイメントなど特定の旅行サービスを予約します。競争的: 複数のエージェントが共有のホテル予約カレンダーを管理し、顧客の予約を競合しながら進めます。                                     |

## AIエージェントを使用するタイミング

前のセクションでは、旅行エージェントのユースケースを使用して、さまざまな種類のエージェントが旅行予約の異なるシナリオでどのように使用されるかを説明しました。このアプリケーションはコース全体で引き続き使用します。

次に、AIエージェントが最適に使用されるユースケースの種類を見てみましょう：

![When to use AI Agents?](../../../translated_images/when-to-use-ai-agents.912b9a02e9e0e2af45a3e24faa4e912e334ec23f21f0cf5cb040b7e899b09cd0.ja.png?WT.mc_id=academic-105485-koreyst)

- **オープンエンドな問題** - ワークフローに常にハードコードできないため、LLMがタスクを完了するために必要なステップを判断する必要がある場合。
- **複数ステップのプロセス** - ツールや情報を複数のターンにわたって使用する必要がある、ある程度の複雑さを持つタスク。
- **時間とともに改善** - 環境やユーザーからのフィードバックを受け取り、より良いユーティリティを提供するために改善できるタスク。

AIエージェントを使用する際のさらなる考慮事項については、「信頼できるAIエージェントの構築」レッスンで詳しく学びます。

## エージェントソリューションの基本

### エージェントの開発

AIエージェントシステムを設計する最初のステップは、ツール、アクション、動作を定義することです。このコースでは、**Azure AI Agent Service** を使用してエージェントを定義する方法に焦点を当てます。このサービスには以下のような特徴があります：

- OpenAI、Mistral、Llamaなどのオープンモデルの選択
- Tripadvisorなどのプロバイダーを通じたライセンスデータの利用
- 標準化されたOpenAPI 3.0ツールの利用

### エージェントパターン

LLMとのコミュニケーションはプロンプトを通じて行われます。AIエージェントは半自律的な性質を持つため、環境の変化後に手動でLLMを再プロンプトする必要がない場合があります。このため、複数ステップでLLMをよりスケーラブルにプロンプトするための **エージェントパターン** を使用します。

このコースでは、現在人気のあるエージェントパターンをいくつか学びます。

### エージェントフレームワーク

エージェントフレームワークを使用すると、開発者はコードを通じてエージェントパターンを実装できます。これらのフレームワークは、テンプレート、プラグイン、ツールを提供し、AIエージェントのコラボレーションをより良くします。これにより、AIエージェントシステムの可観測性やトラブルシューティングの能力が向上します。

このコースでは、研究主導のAutoGenフレームワークと、Semantic Kernelのプロダクション対応エージェントフレームワークを探ります。

**免責事項**:  
この文書は、機械翻訳AIサービスを使用して翻訳されています。正確性を追求していますが、自動翻訳には誤りや不正確さが含まれる可能性があります。元の言語で記載された原文が正式な情報源と見なされるべきです。重要な情報については、専門の人間による翻訳を推奨します。この翻訳の利用によって生じる誤解や解釈の誤りについて、当方は一切の責任を負いません。