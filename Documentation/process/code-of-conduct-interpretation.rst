.. _code_of_conduct_interpretation:

Linux カーネルにおけるコントリビューター行動規範の解釈
================================================================

:ref:`code_of_conduct` は様々なオープンソースコミュニティで普遍的なルールを決めるための文書です。オープンソースコミュニティはそれぞれ異なる性格を持っており、Linux カーネルのコミュニティも例外ではありません。したがって、Linux カーネルコミュニティではコントリビューター行動規範をどのように扱うのかについてこの文書で説明を行います。この文章内での解釈は常に正しいとは限りません。必要に応じて修正が加えられることがあります。

Linux カーネルの開発作業は伝統的なソフトウェア開発とは違って非常に個人的なプロセスを取ります。あなたの貢献と発案は注意深くレビューされ、ときに批難の対象となります。あなたの投稿がカーネルに取り込まれる前に、大抵の場合、レビューによって改善が求められます。このような要求がされるのは Linux にとって最適の解決策が関係者全てに欲されているためです。これまで、この開発プロセスにしたがって、堅牢なオペレーティングシステムのカーネルが作られてきました。品質を損なうようなことは何であれ避けるべきです。

メンテナ
-----------

行動規範では「メンテナ」という言葉が何回も使われています。カーネルコミュニティにおいて、「メンテナ」とはカーネルのソースツリーに含まれる MAINTAINERS に名前が載っている、サブシステム・ドライバー・ファイルを担当している人間を指します。

責任
----------------

行動規範にはメンテナの権限と責任について述べていますが、多少の解題が必要でしょう。

何よりもまず、合理的期待としてメンテナは模範を示します。

ただし、Linux カーネルコミュニティは非常に大規模なので、すでにコミュニティに参加している人々に対してメンテナが一方的に何か慣習を押し付けるということはありません。その責任は私達全てが負うものであり、行動規範による解決を必要とするのは行動に関する未解決の問題の場合で、あくまで最終的な拠り所となるものです。

問題が起こったとき、メンテナは必要に応じてコミュニティの他のメンバーを補助したり協力して問題の解決にあたってください。発生した状況の対処方法がわからない場合はいつでも Technical Advisory Board (TAB) や他のメンテナに協力を仰ぐことができます。あなたが望むのでないかぎり、違反の報告を考慮することはありません。TAB や他のメンテナに協力を求めるべきかどうかわからない場合、調停者である Mishi Choudhary <mishi@linux.com> に連絡してください。

結局のところ、「お互いに親切にすること」が全てのメンバーの最終的な目標です。私達は人間であるがゆえに時として失敗もしますが、問題の平和的解決を第一として協力するべきことに誰しも疑いの余地はありません。行動規範に基づく執行は最終的な手段として存在する、それ以上でもそれ以下でもありません。

Linux カーネルコミュニティの目標は堅牢で技術的に優れたオペレーティングシステムを開発することであり、開発に関わる技術的に複雑な問題を解決するには専門知識と意思決定が必然となります。

必要とされる専門知識は貢献の対象によって変わります。それはまず文脈と技術的な複雑性によって決まり、それから貢献者とメンテナの期待によって決まります。

専門的な期待と意思決定はどちらも議論の対象となりますが、最終的には物事を前に進めるための決定が可能であることが前提となります。この特権はメンテナおよびプロジェクトのリーダーに与えられており、誠実さを持って行使されるべきものです。

特権によって、専門的な期待を持つこと、意思決定をすること、不適切な投稿をリジェクトすることは行動規範の違反とはみなしません。

基本的にメンテナは新しいメンバーの参加を歓迎しますが、貢献者に対してメンテナがハードルを際限なく下げることはできません。メンテナは優先順位を決める必要があります。優先順位の設定もまた、行動規範の違反にはあたりません。カーネルコミュニティはこの問題について kernelnewbies.org などで参加者のレベルに応じたプログラムを用意しています。

適用範囲
----------

Linux カーネルコミュニティでは基本的に公のメーリングリストで連携が取られています。メーリングリストは様々な団体や個人によって運営されている数々のサーバー上に存在します。メーリングリストは全てカーネルソースツリー内の MAINTAINERS ファイルに載っています。記載されているメーリングリストに送信されるメール全てに対して行動規範が適用されます。

kernel.org の bugzilla や他のサブシステムの bugzilla、あるいは他のバグトラッキングシステムを使っている開発者も行動規範のガイドラインに従ってください。Linux カーネルコミュニティには「公式の」プロジェクトメールアドレスあるいは「公式の」ソーシャルメディアアカウントが存在しません。会社のメールアカウントを使用している個人が会社のルールに従わなければならないように、kernel.org メールアカウントを使用したあらゆる活動は行動規範に従わなければなりません。

メーリングリストのメッセージ、カーネルの変更履歴メッセージ、あるいはコードのコメント内に名前・メールアドレス・関連するコメントを付することは行動規範によって禁止されません。

他のフォーラムにおける投稿はそのフォーラムが準じているルールが適用され、基本的に行動規範の対象外となります。ただし特別な事情がある場合はその限りではありません。

カーネルに貢献する場合は適切な言葉を使ってください。行動規範が採択される以前に存在したコンテンツについては現時点で違反による修正対象となることはありません。ただし、不適切な言葉はバグとして扱われる可能性があります。そのようなバグは関係者がパッチを投稿した際に速やかに修正されるものとします。ユーザー/カーネル API に含まれている表現、標準や仕様で用いられている用語はバグとはみなされません。

執行
-----------

行動規範に記載されているアドレスに送信したメールは行動規範委員会に届きます。メールを受け取るメンバーの一覧は https://kernel.org/code-of-conduct.html に記載されます。委員会に参加していないメンバーは報告を閲覧できません（委員会を脱会後も閲覧不可となります）。

行動規範委員会の初期メンバーは TAB のボランティア、中立的な第三者として活動する職業上の仲裁者から構成されます。委員会の最初の任務はプロセスを文章化して、公開することになります。

委員会に属するメンバー全員には報告を行いたくない場合、仲裁者を含む委員会のメンバーのいずれかに直接連絡を取ることも可能です。

行動規範委員会はプロセス (上述) に従って事態を判断し、必要に応じて TAB と意見を交換します。例えばカーネルコミュニティの情報を入手したい場合などが適切とされます。

委員会による決定は TAB に提出され、必要に応じて関連するメンテナに執行されます。行動規範委員会による決定は TAB の3分の2以上の投票によって覆されます。

四半期ごとに、行動規範委員会と TAB は行動規範委員会が受け取った報告（報告者は匿名で扱います）と現状、さらに覆された決定の詳細と投票の内訳について報告します。

行動規範委員会の設立からプロセスは変わっていくことが想定されます。この文章はプロセスの変化に応じて情報が更新されます。
