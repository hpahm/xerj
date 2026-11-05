# XERJ

**XERJ: công cụ tìm kiếm cho AI agent.** Một cách mới để AI tìm dữ liệu: một tệp nhị phân Rust local duy nhất lập chỉ mục mã nguồn, tài liệu, đặc tả và log của bạn, cùng các gói Corpus Hub, và trả về câu trả lời có trích dẫn.

**Máy tìm kiếm local-first và máy chủ MCP cho AI agent.** Một tệp nhị phân Rust lập chỉ mục mã nguồn, tài liệu, log, JSONL/CSV và PDF cho BM25 full-text, vector và hybrid search, code search và bộ nhớ agent, nằm sau API tương thích Elasticsearch. Hoạt động với Claude Code, Cursor và bất kỳ client MCP nào.

<a href="https://trendshift.io/repositories/116361?utm_source=repository-badge&amp;utm_medium=badge&amp;utm_campaign=badge-repository-116361" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/repositories/116361/status.svg" alt="Trendshift" /></a>

[English](./README.md) | [简体中文](./README.zh-CN.md) | [日本語](./README.ja-JP.md) | [العربية](./README.ar.md) | [Español](./README.es.md) | [한국어](./README.ko.md) | [فارسی](./README.fa.md) | [Tiếng Việt](./README.vi.md)

[![CI](https://img.shields.io/github/actions/workflow/status/xerj-org/xerj/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/xerj-org/xerj/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/xerj-org/xerj?style=flat-square&label=release)](https://github.com/xerj-org/xerj/releases)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue?style=flat-square)](./LICENSE)
[![Stars](https://img.shields.io/github/stars/xerj-org/xerj?style=flat-square)](https://github.com/xerj-org/xerj/stargazers)
[![Rust](https://img.shields.io/badge/built%20with-Rust-000000?style=flat-square&logo=rust)](https://www.rust-lang.org)
[![Discussions](https://img.shields.io/github/discussions/xerj-org/xerj?style=flat-square&label=discussions)](https://github.com/xerj-org/xerj/discussions)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.com/invite/yetXFusXfs)
[![X](https://img.shields.io/badge/X-%40xerj__org-000000?style=flat-square&logo=x&logoColor=white)](https://x.com/xerj_org)

[![Reference coding](https://img.shields.io/badge/reference%20coding-2.7%C3%97%20fewer%20tokens-ff8c00?style=flat-square)](https://xerj.org/case-studies/reference-coding.html)
[![Autoindex](https://img.shields.io/badge/autoindex-zero%20config-ff8c00?style=flat-square)](https://xerj.org/docs/cli.html)
[![Search](https://img.shields.io/badge/search-BM25%20%2B%20kNN%20%2B%20hybrid-8957e5?style=flat-square)](https://xerj.org/docs/queries.html)
[![Agent memory](https://img.shields.io/badge/agent%20memory-%2F__memory-00b3a4?style=flat-square)](https://xerj.org/docs/recipes/agentic-memory.html)
[![MCP](https://img.shields.io/badge/MCP-native-1f6feb?style=flat-square)](https://xerj.org/llms.txt)
[![llms.txt](https://img.shields.io/badge/llms.txt-agent%20ready-6f42c1?style=flat-square)](https://xerj.org/llms.txt)
[![ES-YAML conformance](https://img.shields.io/badge/ES--YAML%20conformance-1444%2F1454-brightgreen?style=flat-square)](https://xerj.org/benchmarks)
[![Single static binary](https://img.shields.io/badge/single%20static%20binary-no%20JVM-orange?style=flat-square)](https://xerj.org/docs/install.html)
[![Default embedder](https://img.shields.io/badge/default%20embedder-lexical%2C%20offline-teal?style=flat-square)](https://xerj.org/docs/vectors.html)
[![Neural](https://img.shields.io/badge/neural%20embedder-opt--in%2C%20downloads%20~90%20MB-9c6ade?style=flat-square)](https://xerj.org/docs/vectors.html)

XERJ là một công cụ tìm kiếm AI local được cộng đồng tin tưởng, tự động lập chỉ mục bất kỳ thư mục nào, giúp AI agent không còn tốn token để đọc từng file một mà truy xuất đúng đoạn mã cần thiết thay vì phải lướt qua kho dữ liệu. Reference coding là trường hợp sử dụng chính và lợi ích rõ nhất: hướng một agent tới một nhiệm vụ, nó sẽ tải xuống các repo mã nguồn mở gần nhất, lập chỉ mục và tái sử dụng cách giải quyết tương tự trước khi viết riêng. Trong một nghiên cứu kiểm soát, nó giảm 2.7x số token output của agent đi cùng tỷ lệ giải quyết 16/16 ([case study](https://xerj.org/case-studies/reference-coding.html)), và người dùng báo cáo giảm khoảng 5x trong công việc hàng ngày ([field reports](./user-feedback/11-reference-coding-field-reports/2026-08-11-token-savings-reports.md)).

Với một mô hình nhỏ hơn, rẻ hơn, XERJ có thể vượt qua mô hình đắt tiền hơn khi làm việc từ trí nhớ, đồng thời bạn bỏ ít thời gian hơn trong vòng lặp sửa lỗi. Hãy thử ngay bằng một câu lệnh cài đặt:

```text
Cài đặt XERJ (docs: https://xerj.org/llms.txt), lập chỉ mục mã nguồn của dự án này, và thiết lập
reference coding: clone và lập chỉ mục các repo mã nguồn mở gần nhất với những gì chúng ta đang xây dựng,
 rồi tìm cách họ giải quyết vấn đề trước khi viết code.
```

Hoặc chạy trực tiếp:

```sh
curl -fsSL https://xerj.org/get | sh
xerj --insecure --data-dir ~/xerj-data &
xerj init                                        # kết nối XERJ vào Claude Code/Cursor (MCP + skill), một lệnh
xerj autoindex ~/my-project
xerj search "how do we rotate the WAL segment"   # passages xếp hạng, file:line
xerj def "euler_to_rotationmatrix"               # go-to-definition: file:line + signature
xerj gain                                        # những gì nó đã làm cho bạn — được tính, không ước lượng
```

Giữ thư mục dữ liệu ngoài bất kỳ thư mục nào bạn sẽ dùng `autoindex`. Thư mục `data/` không nằm trong danh sách ignore mặc định, nên nếu `--data-dir ./data` nằm trong cây thư mục bạn sắp index thì node sẽ lập chỉ mục kho lưu trữ của chính nó.

Khi khởi động, `Data dir` hiển thị đường dẫn tuyệt đối đã giải quyết, `Data source` cho biết cờ đã chọn, file cấu hình được chọn hoặc mặc định, và `Data status` cho biết liệu lần khởi động này đã tạo thư mục hay chưa. Một thư mục mới có thể khiến node cũ xuất hiện thiếu chỉ mục hoặc tài khoản chủ sở hữu: hãy khởi động lại bằng `--data-dir` hoặc `--config` cũ. XERJ không tự phát hiện hay migrate dữ liệu từ các data directory khác.

Cờ `--insecure` là ranh giới tin cậy, không phải nghi thức. Nó tắt TLS và xác thực API key, nên mọi caller nào có thể truy cập cổng đều trở thành superuser và có thể đọc, xóa mọi index, bao gồm mọi namespace `/_memory`. Nó dành cho một người dùng trên máy dev: một node mới chỉ bind `127.0.0.1`, và bind rõ text trên interface khác sẽ từ chối khởi động trừ khi bạn chủ động cho phép. Mô hình đầy đủ ở [docs/SECURITY_MODEL.md](./docs/SECURITY_MODEL.md).

## Tham gia cộng đồng

Bạn gia nhập XERJ bằng cách chạy nó và gửi lại một báo cáo ngắn về trải nghiệm: một commit hoặc một PR. Báo cáo đó là "thẻ thành viên" và là điều duy nhất dự án yêu cầu đổi lại cho một binary Apache-2.0 miễn phí. Đó là thứ giữ cho engine cải thiện cho ngư���i dùng tiếp theo.

Cả con người và AI agents đều được chào đón; đây không phải là dự án chỉ dành cho agents. Dù bạn đã index một repo trong giờ nghỉ trưa hay một agent đã cài XERJ giữa chừng trong dự án của người khác, yêu cầu vẫn giống nhau: một báo cáo ngắn mô tả bạn đã chỉ vào đâu, dùng nó để làm gì, và đánh giá thật lòng. Đánh giá tiêu cực cũng là báo cáo tốt. Nếu có điều gì đó bị hỏng, đó là một issue hoặc fix riêng.

Field-report PRs được CLA-exempt, nên merge mà không cần chữ ký. Đường dẫn hoạt động trên mọi build là một `gh pr create` đơn giản, thêm đúng một markdown file trong [`user-feedback/16-agent-field-reports/`](./user-feedback/16-agent-field-reports) và không có gì khác trong diff. Nếu build có hỗ trợ, `xerj feedback` sẽ soạn báo cáo và điền version, OS và thứ đã được index, và `xerj feedback --open-pr` mở PR cho bạn. Xem `xerj --help` để kiểm tra binary của bạn có lệnh này không.

## Lý do có thể đo được: reference coding

Một agent dùng grep sẽ kéo cả file vào context, lên đến 1.06M input tokens trên một corpus trong đo lường của chúng tôi, và vẫn phải đọc chúng. Một agent truy vấn XERJ chỉ nhận được đoạn passage. Đo từ đầu đến cuối trên mã mà model chưa nhớ ([case study](https://xerj.org/case-studies/reference-coding.html): 8 task, 4 ngôn ngữ, 16 lượt chạy mỗi nhánh, token thực tế từ `claude -p`):

| | output tokens | chi phí | giải quyết |
|---|---:|---:|---:|
| chỉ từ trí nhớ | 260,916 | $11.18 | 11/16 |
| agent chạy grep | 26,477 | $3.27 | 16/16 |
| XERJ | 9,982 | $1.58 | 16/16 |

Nói cách khác, XERJ dùng 2.7x ít output tokens hơn grep và 26x ít hơn trí nhớ đơn thuần ở cùng tỷ lệ giải quyết, và lên tới 278x ít hơn trên một task Java duy nhất. Trong phát triển thực tế, người dùng báo cáo khoảng 5x ít token hơn từ đầu đến cuối ([field reports](./user-feedback/11-reference-coding-field-reports/2026-08-11-token-savings-reports.md)).

Giá trị của nó bị giới hạn bởi khả năng nhớ: nó thắng trên code riêng tư, nội bộ, niche hoặc sau cutoff, và trung tính đến có hại trên các thư viện công khai phổ biến mà model đã biết. Sự hạn chế trung thực nằm ở [case study](https://xerj.org/case-studies/reference-coding.html).

## Cho nó bất kỳ thư mục nào

Reference coding là một trường hợp sử dụng của cùng một primitive: `xerj autoindex <folder>` khiến agent biết một corpus thay vì grep nó. Chỉ một lệnh là đủ để index mã nguồn, tài liệu, log, PDF, SQLite và CSV bất thường thành các index có kiểu, có thể truy vấn cho search, RAG, security audit và agent memory, không cần viết schema và không cần pipeline.

```sh
xerj --insecure --data-dir ~/xerj-data &      # khởi động
xerj autoindex ~/my-project              # trỏ tới bất cứ thứ gì
```

`--insecure` ở đây lại đồng nghĩa là không TLS, không auth — mọi caller đều là superuser — nên đây là cùng một ranh giới single-user-on-dev-machine như trên ([security model](./docs/SECURITY_MODEL.md)).

XERJ dò mọi file, xác định đó là gì, và tạo một index cho mỗi dataset nó tìm thấy. Mã code đi qua tree-sitter nên có symbol và line number, không chỉ text thô:

```
phase A: 593 datasets inferred, 1955 junk/skipped files
phase B: indexing 25329 files with 8 workers
done in 158.1s, 593 datasets, 83103 records live, 790 junk records
```

Chia sẻ một data map ngoại tuyến với `xerj autoindex map --prefix myproject --html xerj-map.html --redact-paths`, hoặc dùng `--md xerj-map.md` cho Markdown. Báo cáo bao gồm số lượng dataset, tên symbol, graph hubs khi có, thông tin file bị bỏ qua và gợi ý tìm kiếm. Xem lại tên metadata trước khi chia sẻ. [Ví dụ, phạm vi quyền riêng tư và cách tái tạo](tools/map-report/README.md).

## Mọi người hay dùng nó cho điều gì

- Reference coding: index các project OSS gần vấn đề nhất và truy xuất cách họ đã giải quyết trước khi viết code (use case đo được ở trên).
- Codebase Q&A và RAG: index một repo, hỏi về cơ chế, và nhận đoạn passage kèm `file:line` thay vì liệt kê thư mục.
- Security audits: index cây mục tiêu và truy vấn pattern sink, secret và call nguy hiểm trên mọi loại file cùng lúc.
- Log và incident analysis: các định dạng hỗn hợp trở thành index có kiểu với các aggregation mà bạn mong đợi từ Elasticsearch.
- Agent long-term memory: `/_memory/{namespace}` lưu những gì agent học được và gọi lại bằng nghĩa trong session tiếp theo.

## Prompt hoạt động như thế nào

[llms.txt](https://xerj.org/llms.txt) cung cấp cho agent các bước theo thứ tự: cài đặt, khởi động server, `xerj autoindex .`, query bằng bất kỳ Elasticsearch client nào, và vòng lặp reference-coding (clone project OSS tương tự, index, truy xuất cơ chế trước khi viết, trích dẫn những gì dùng, tôn trọng license).

Lý do nó hữu ích: một agent làm việc từ trí nhớ sẽ lặp lại vòng lặp thử sai trên bất kỳ API nào nó chưa ghi nhớ, và grep chỉ cho nó biết nên xem ở đâu; việc khôi phục vẫn là đọc source vào context, lên đến 1.06M input tokens trên một corpus trong đo lường của chúng tôi. Một agent truy vấn XERJ đọc đúng passage thay vì phải đọc file.

Một số prompt hoạt động trên máy cài mới:

- *"Đọc https://xerj.org/llms.txt, đặt XERJ làm backend tìm kiếm, index `./docs`, và cho tôi xem một ví dụ query cho mỗi index đã tạo."*
- *"Chạy `xerj autoindex map` và cho tôi biết dữ liệu này có gì (loại, số lượng và những caveat đã ghi nhận), sau đó trả lời câu hỏi bằng search thay vì đọc file."*
- *"Dùng API `/_memory/notes` của XERJ như long-term memory cho dự án này: lưu những gì bạn học được khi làm việc, và recall bằng nghĩa trong session tiếp theo."*

Ví dụ đã hoạt động, được validate cho mỗi capability: [xerj.org/docs/recipes](https://xerj.org/docs/recipes/).

<video src="https://xerj.org/xerj-biz-demo.mp4" poster="docs/media/demo-poster.png" controls muted playsinline width="840">
  <a href="https://xerj.org/aise-demo.html"><img src="docs/media/demo-poster.png" width="840" alt="Xem demo XERJ: khởi động, ingest, search, vectors, dashboards"></a>
</video>

<sub>Khởi động, bulk ingest, search, vector kNN, dashboard trực tiếp, không cắt.
<a href="https://xerj.org/aise-demo.html">Xem trên xerj.org</a> hoặc
<a href="https://xerj.org/playground/">thử playground trực tiếp</a>.</sub>

## Cài đặt theo cách thủ công

```sh
curl -fsSL https://xerj.org/get | sh
```

Windows PowerShell:

```powershell
irm https://xerj.org/get.ps1 | iex
```

Nix (build từ source; `nix develop` mở shell với Rust toolchain):

```sh
nix run github:xerj-org/xerj -- --version
```

Một binary tĩnh, không JVM, không dependency. Có build sẵn cho Linux, macOS và Windows trên x86-64 và arm64. X86-64 build nhắm tới x86-64-v2 (SSE4.2: Intel Nehalem 2008 và sau đó, AMD Bulldozer và sau đó), và dùng AVX2 và FMA ở runtime khi CPU có chúng, nên máy cũ hơn Haswell vẫn chạy cùng binary. Nó nói giao thức Elasticsearch, nên client, dashboard và tooling hiện có làm việc mà không cần sửa.

Các lệnh đầu tiên sau khi cài đặt (installer in ra nơi `xerj` nằm; thêm vào PATH nếu cần): `xerj --insecure --data-dir ~/xerj-data &`, chờ cho `http://localhost:9200` phản hồi, rồi gõ `xerj autoindex ~/my-project`. Xem [Index a folder](#index-a-folder).

Đối với host không có internet runtime, làm theo [air-gapped deployment recipe](./docs/recipes/air-gapped-deployment.md). Default lexical embedder là offline; neural mode cần ba model file được staging sẵn trước khi thực hiện semantic operation đầu tiên.

## Index một thư mục

Khởi động server, sau đó truyền `autoindex` tới bất kỳ thứ gì:

```sh
xerj --insecure --data-dir ~/xerj-data &     # local dev: no TLS, no auth
xerj autoindex ~/my-project
```

Đây là ranh giới tin cậy dev-machine từ đầu README — không TLS, không auth, mọi caller đều là superuser. Nó phù hợp trên laptop vì node mới chỉ bind `127.0.0.1` và không bind gì khác; shared host muốn auth-on start ở ngay dưới đây.

Nếu server của bạn đang bật auth, đây là default cho mọi start không có `--insecure` (bao gồm bất kỳ start từ config file nào), hãy truyền cùng một key cho `autoindex`. Nó không lấy key từ `xerj.toml`; hãy truyền `--api-key` hoặc đặt `XERJ_API_KEY`, hoặc mọi request sẽ trả `401 Unauthorized`:

```sh
xerj --data-dir ~/xerj-data &                          # auth on: key minted on first boot
export XERJ_API_KEY="$(cat ~/xerj-data/admin.key)" # <data_dir>/admin.key
xerj autoindex ~/my-project
```

Đó là toàn bộ setup. Không có schema cần viết và không có pipeline cần cấu hình. XERJ dò từng file, xác định loại file, và tạo một index cho mỗi dataset nó tìm thấy:

```
phase A: 593 datasets inferred, 1955 junk/skipped files
phase B: indexing 25329 files with 8 workers
done in 158.1s, 593 datasets, 83103 records live, 790 junk records
```

Source files đi qua tree-sitter, nên code đến với symbol và line number thay vì chỉ là text phẳng. CSV, JSON, JSONL, XML, YAML, SQLite, PDF, DOCX, PowerPoint (`.pptx`, một record mỗi slide), Excel (`.xlsx`, một dataset mỗi sheet), EPUB books (một record mỗi chapter), Jupyter notebooks (một record mỗi heading section, bất kỳ kernel nào), man pages (roff, một record mỗi section), HTML, mail (`.eml` và mbox mailbox, bao gồm Google Takeout export) và các log format phổ biến đều được xử lý. Unity projects có xử lý đầu tiên: text-serialized scenes, prefabs và assets trở thành một record cho mỗi GameObject/Component, `.meta` files trở thành bảng GUID-to-path, và MonoBehaviour records mang `script_class`/`script_path` để "các scene nào dùng script này?" chỉ cần một query (binary-serialized assets cần Force Text mới đọc được; generated dirs như `Library/` được auto-skipped và ghi nhận).

## Tìm kiếm

Đây là Elasticsearch API, nên bạn đã biết phần này:

```sh
# nó tìm thấy cái gì?
curl localhost:9200/_cat/indices

# full-text
curl "localhost:9200/ax-*/_search?q=checkout+error"

# structured
curl localhost:9200/ax-orders/_search -H 'content-type: application/json' -d '{
  "query": { "range": { "total": { "gte": 100 } } },
  "aggs":  { "by_status": { "terms": { "field": "status" } } }
}'
```

Vector và hybrid search dùng cùng cú pháp `knn` và `semantic` mà bạn gửi tới Elasticsearch. Bất kỳ Elasticsearch client library nào cũng sẽ hoạt động nếu bạn trỏ vào `localhost:9200`.

## Chấm điểm kết quả với Jev

Một search score cho biết kết quả nào đứng trên kết quả nào, nhưng không nói liệu kết quả đó thực sự trả lời câu hỏi hay không. [Jev](https://typesafe.ai/blog/introducing-system-one-models-and-jev), một service của TypeSafe AI, làm việc đó: cho một câu hỏi và một document và nó trả về số từ 0 đến 1, độ phù hợp của document với câu hỏi. XERJ làm việc với Jev theo hai cách.

**1. Sắp xếp lại kết quả bằng Jev (tùy chọn).** Thêm `"rerank": {}` vào `_search` và XERJ sẽ gửi top results tới Jev, rồi sắp xếp theo con số nhận được. Trên bộ test FiQA công khai, chất lượng kết quả tăng từ 0.24 lên 0.36 (nDCG@10), với chi phí khoảng $0.64 cho tổng cộng 648 searches. Hãy coi các con số là cách sắp xếp, không phải phần trăm chính xác: chúng không được hiệu chuẩn tốt.
**Điều này gửi text của các kết quả đó lên máy chủ TypeSafe.** Nó ở trạng thái tắt cho đến khi bạn đặt key, và `[rerank] enabled = false` cấm hoàn toàn. Đọc [`docs/RERANK.md`](./docs/RERANK.md) trước khi bật.

**2. Nhận cùng loại câu trả lời ở local.** `POST /v1/systemone` và `POST /_decide` chấp nhận cùng câu hỏi và cùng định dạng, nhưng XERJ tự trả lời bằng cách tìm những document tương tự nhất mà bạn đã gắn nhãn trước đó (ví dụ các tin nhắn đã được đánh dấu spam hay không). Không dữ liệu nào rời khỏi máy bạn và không cần key. Nó chỉ hoạt động nếu bạn có examples đã gắn nhãn; trên AG News (120k examples đã gắn nhãn) nó chọn nhãn đúng 92% thời gian. Client Python chính thức `jev-reranker` hoạt động với node XERJ mà không thay đổi ([test](./benchmarks/systemone-gate)). XERJ trả lời dưới tên riêng của mình, `xerj-history-vote-1`; nó không phải Jev.

Các phép đo và cách tái tạo: [`benchmarks/beir-hybrid`](./benchmarks/beir-hybrid/results/2026-09-20-rerank-full-fiqa) và [`benchmarks/decisions-as-retrieval`](./benchmarks/decisions-as-retrieval).

## Kết nối agent qua MCP

Không phải agent nào cũng có thể chạy shell command. Các assistant trên desktop và các host hỗ trợ function-calling tiếp cận tools qua Model Context Protocol, và binary bạn vừa cài là MCP server. Không có gì phải download thêm và không cần compile:

```sh
xerj --insecure --data-dir ~/xerj-data &     # 1. node mà tools query
xerj mcp                                # 2. MCP stdio server (client của bạn chạy lệnh này)
```

`xerj mcp` nói MCP qua stdio và proxy tới node được đặt bởi `XERJ_URL` (mặc định `http://localhost:9200`). Nó không khởi động node; bước 1 ở trên là điều kiện tiên quyết. MCP server không thêm bất kỳ trust nào của riêng nó — nó là cùng binary nói stdio với client và HTTP thuần với node, nên ranh giới của node mới là thứ quan trọng, và bước 1 ở trên khởi động cùng một dev node `--insecure`. Đưa đoạn dưới vào config của client MCP:

```json
{
  "mcpServers": {
    "xerj": {
      "command": "/home/you/.local/bin/xerj",
      "args": ["mcp"],
      "env": { "XERJ_URL": "http://localhost:9200" }
    }
  }
}
```

Dùng đường dẫn tuyệt đối. Trình cài `sh` (Linux, macOS và Windows Git Bash, MSYS và Cygwin) đặt `xerj` vào `~/.local/bin` (`xerj.exe` trên Windows; `command -v xerj` xác nhận) và không sửa PATH.

Nếu node đang chạy với auth (mọi start ngoại trừ `--insecure`), thêm `"XERJ_AUTH": "ApiKey <key>"` cùng `XERJ_URL`; key nằm ở `<data-dir>/admin.key`.

## Vì sao nó tồn tại

Agents tiêu tốn context window để đọc file. PHP trong WordPress core khoảng 5.2 triệu tokens, tương đương 26 full context windows, nên agent không thể chỉ đơn giản đọc hết. Grep cũng không giải quyết được, vì grep hit chỉ là một dòng, và để đánh giá dòng đó thì vẫn phải mở cả file.

Querying một index chỉ tốn vài KB cho mỗi câu hỏi. Trong [một cuộc AI security audit của WordPress core](https://xerj.org/use-cases/code-security-audit.html), một agent làm việc trên 1,492 file PHP và chỉ dùng khoảng 26,000 tokens, tương đương lượng cần để load khoảng nửa phần trăm cây.

## Use cases

- [Reference coding](https://xerj.org/case-studies/reference-coding.html): agent lập trình truy xuất cách các project peer đã giải quyết nó thay vì tự suy ra lại. Đo được 2.7x ít output tokens hơn grep-driven coding (26x so với memory alone).
- [Code search và security audits](https://xerj.org/use-cases/code-security-audit.html): index AST-aware, nên agent tìm thấy function thay vì chỉ một dòng.
- [AI search và RAG](https://xerj.org/use-cases/ai-search-retrieval.html): full-text, vector và hybrid retrieval trong một query, không cần vector database riêng.
- [Agent memory](https://xerj.org/use-cases/second-brain.html): recall lâu dài với knowledge graph trên tài liệu của riêng bạn.
- [Log analytics và observability](https://xerj.org/use-cases/unified-observability.html): logs, metrics và traces trong cùng một engine.
- [Elasticsearch replacement](https://xerj.org/use-cases/elasticsearch-replacement.html): cùng wire protocol, một binary.

Ví dụ có thể chạy nằm trong [`recipes/`](./recipes) và [`docs/examples/`](./docs/examples).

## Tương thích Elasticsearch

XERJ triển khai Elasticsearch REST API: indices, documents, bulk, search, aggregations, mappings, kNN, scroll, reindex và các endpoint `_cat`. Kibana và client libraries chính thức kết nối trực tiếp với nó. Một ranh giới đáng biết trước khi trỏ export tooling vào nó: scroll là snapshot up-front có giới hạn, không phải cursor duyệt segment, nên query mà total chính xác vượt quá snapshot window sẽ bị từ chối với `400` thay vì silently truncated. Dùng `search_after` cho result set kích thước lớn hơn ([giới hạn](https://xerj.org/docs/api-es-compat.html#scroll-cap)).

Bộ conformance suite chạy trên mọi commit và hiện đang pass 1444/1454 cases (0 failed, 10 skipped). Nó nằm trong [`engine/tests/es-compat-yaml`](./engine/tests/es-compat-yaml), và các gap còn lại được liệt kê ở đó thay vì giấu đi. XERJ tương thích với API. Nó không phải reimplementation của Elasticsearch internals, và cũng không phải fork.

## Benchmarks

XERJ được benchmark trực tiếp với Elasticsearch 8.13.4 trên ingest, full-text search, aggregations, vector search và đọc khi có write flood đồng thời. Run closed-loop mới nhất ghi 55 wins, 26 ties, 4 losses, bao gồm 1.72x ingest throughput và 1.61x footprint nhỏ hơn trên đĩa.

Tất cả 4 losses cùng là một gap: read p99 trong lúc writer tốc độ cao chạy. Nó được [ghi đầy đủ](./demo/playbooks/MIXED_READ_UNDER_WRITE_FINDING_2026-07-08.md) thay vì giấu đi. Kết quả, methodology và harness ở [xerj.org/benchmarks](https://xerj.org/benchmarks) và trong [`demo/playbooks`](./demo/playbooks), nên bạn có thể chạy lại. Hãy coi mọi con số không thể tái tạo được như không đáng tin cậy, kể cả của chúng tôi.

### Code indexing

Source files được parse bằng tree-sitter và đánh index AST-aware — symbols plus full text — nên agent truy xuất function, không phải một dòng. Trên checkout Apache Lucene (6,113 source files, 51 MB), single-threaded in-process extraction chạy khoảng **~1,500 files/s (13 MB/s)**; tree-sitter parse chiếm khoảng 72% và là per-file floor. Có thể tái tạo bằng:

```sh
XERJ_EXTRACT_BENCH=/path/to/repo cargo test -p xerj-autoindex --release \
  extract_bench -- --nocapture --ignored
```

Re-indexing là **incremental**: một file mà nội dung byte-identical với generation đã index lần trước sẽ skip parsing hoàn toàn và giữ kết quả đã commit. Vì vậy, chạy lại sau khi sửa vài file sẽ chỉ làm việc tương ứng với phần thay đổi, không phải cả repo — trường hợp edit-and-rerun / CI rất phổ biến, thường >95% unchanged. Toàn bộ content hash vẫn chạy để phát hiện thay đổi, nên thời gian re-index floor vẫn là hashing, không phải parsing.

## Build từ source

Bạn cần Rust toolchain ổn định.

```sh
git clone https://github.com/xerj-org/xerj
cd xerj/engine
cargo build --release -p xerj-server
./target/release/xerj --insecure --data-dir ~/xerj-data
```

Các build x86-64 release target `x86-64-v2` (SSE4.2; cài per target trong `engine/.cargo/config.toml`). HNSW dot-product kernel cũng compile phiên bản AVX2+FMA và chọn runtime khi CPU có cả đặc tính. `RUSTFLAGS` ghi đè file đó, nên local build có thể chọn CPU host:

```sh
RUSTFLAGS="-C target-cpu=native" cargo build --release -p xerj-server
```

Để chạy conformance suite chống lại server đang chạy:

```sh
cargo run --release -p es-yaml-runner -- --dir tests/es-compat-yaml/yaml
```

## Tài liệu

- [Hướng dẫn và API reference](https://xerj.org/docs/)
- [Recipes](https://xerj.org/docs/recipes/) cho các tác vụ phổ biến
- [Roadmap](./ROADMAP.md): chức năng nào đã ship và chức năng nào đang tới, được kiểm tra đối chiếu với binary release. Xem theo version:
  [milestones](https://github.com/xerj-org/xerj/milestones); trạng thái trực tiếp:
  [project board](https://github.com/users/xerj-org/projects/1); điểm tham chiếu đứng:
  [pinned roadmap issue](https://github.com/xerj-org/xerj/issues/298)
- [Changelog](./CHANGELOG.md)

Các trang reference cho từng subsystem, viết dựa trên source và bao gồm các giới hạn mà mỗi phần không nâng lên:

- [Second brain](./docs/SECOND_BRAIN.md) cho relationship layer trên indexed documents: `/_graph` routes, evidence trên links, tám detector và giới hạn two-hop.
- [Console reader](./docs/CONSOLE_READER.md) cho corpus home của console, reader cho bất kỳ record nào (email với attachment, PDF page) và read-only guest mode, với các rendering rules giữ document độc hại vô hại và những thứ nó không render.
- [Scripting](./docs/SCRIPTING.md) cho Painless subset, nơi scripts chạy, và resource limits giới hạn chúng.
- [Snapshot and restore](./docs/SNAPSHOT_AND_RESTORE.md) cho subset API snapshot được hỗ trợ, và restore thay thế những gì.
- [Sharing](./docs/SHARING.md) cho `xerj share`: guest access read-only tới một indexed folder qua link và passcode, điều guest có thể và không thể truy cập, và threat model.
- [Security model](./docs/SECURITY_MODEL.md) cho authentication, reserved `.xerj-memory-*` namespace, API keys và những thứ không được enforce.
- [Reranking](./docs/RERANK.md) cho optional `rerank` search stage: một external judge tái sắp xếp top hits theo probability đã hiệu chuẩn. Đây là feature duy nhất ở search-time gửi text document ra ngoài node (proxy embeddings và WAL tap cũng gửi text khi operator cấu hình), nó cần provider key do operator cấu hình, và chất lượng ranking với model thật không được verify.
- [XERJ vs Lucene 10.3.1](./docs/XERJ_VS_LUCENE.md) cho so sánh source-pinned, sáu trục, về thiết kế storage và search.

## Đóng góp

Pull requests được chào đón từ cả con người và AI agents; xem [Tham gia cộng đồng](#tham-gia-cộng-đồng) ở trên. Baseline contribution là một field report ngắn: một `gh pr create` đơn giản thêm một markdown file trong [`user-feedback/16-agent-field-reports/`](./user-feedback/16-agent-field-reports).

Field-report-only PRs được CLA-exempt, nên merge mà không cần ký tên.

Đối với code changes, xem [CONTRIBUTING.md](./CONTRIBUTING.md) cho workflow, và [CLA.md](./CLA.md) cho contributor licence agreement, chỉ cần một chữ ký cho mỗi contributor chứ không phải mỗi pull request. Agent mở PR nên nói rõ rằng một agent đã viết nó và tuân theo [AGENTS.md](./AGENTS.md) / [.github/AI_CONTRIBUTIONS.md](./.github/AI_CONTRIBUTIONS.md).

Bugs và feature requests gửi tới [GitHub issues](https://github.com/xerj-org/xerj/issues).

## Giấy phép

[Apache 2.0](./LICENSE).
