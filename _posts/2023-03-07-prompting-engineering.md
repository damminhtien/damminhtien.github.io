---
title: Về prompt engineering
tags: GPT prompting prompt-engineering
---

@Author: damminhtien :whale:

@LastUpdate: 07/03/2023

[Prompting engineering](https://en.wikipedia.org/wiki/Prompt_engineering) xuất hiện trong khoảng < 2 năm gần đây như là một kỹ năng mới trong tương lai mà mọi người đều cần học và giỏi nó. Với sự phát triển mạnh của khoa học hàn lâm và marketing  về các ngôn hình ngôn ngữ lớn
(Large Language Model - LLMs), kỹ thuật prompting lại càng trở nên quan trọng và nó đang kiếm tiền được rất nhiều tiền.

Một startup ở San Francisco, Mỹ đang [tuyển dụng người viết promt](https://jobs.lever.co/Anthropic/e3cde481-d446-460f-b576-93cab67bd1ed) với mức lương khoảng 175k-335k USD (tương đương ~4-8 tỉ VND) một năm. Anthropic là một trong những công ty dẫn đầu về các mô hình LLMs đang gặp nhiều vấn đề khi tuyển dụng vị trí này.

Về cơ bản, kỹ thuật prompting là một phương pháp sử dụng ngôn ngữ tự nhiên để tương tác với các mô hình ngôn ngữ lớn (LLMs) như GPT-3, và khai thác khả năng của chúng để tạo ra các dự đoán và phân tích văn bản. Phương pháp này yêu cầu sử dụng các câu hỏi hoặc yêu cầu được viết bằng ngôn ngữ tự nhiên để gợi ý cho mô hình và định hướng quá trình tạo ra đầu ra. Kỹ thuật prompting có thể được sử dụng để giải quyết nhiều loại vấn đề khác nhau, từ phân tích ngôn ngữ tự nhiên đến dự đoán văn bản và thiết kế kiến trúc mạng mới.

Khi viết prompt, người viết cần có kiến thức và hiểu biết về lĩnh vực liên quan đến nội dung mà họ muốn tạo ra prompt. Họ cần biết rõ đối tượng sử dụng prompt và mục đích sử dụng của họ. Ngoài ra, người viết prompt cần có kỹ năng viết văn bản tốt để tạo ra các câu hỏi hoặc yêu cầu có ý nghĩa, đưa ra thông tin cần thiết và tránh những sự hiểu nhầm hoặc mâu thuẫn. Họ cũng cần hiểu các kỹ thuật và công cụ liên quan đến prompting để tạo ra prompt hiệu quả.
Tham khảo thêm tại [promp engineering guide](https://github.com/dair-ai/Prompt-Engineering-Guide)

Ngoài ra cũng có rất nhiều mẫu prompt hay được tổng hợp lại từ cộng đồng trên thế giới. Bạn có thể xem tại [awesome chatgpt prompt](https://github.com/f/awesome-chatgpt-prompts).

Trong phần tiếp theo, tôi dịch lại từ trang [Data Machina số #191](https://datamachina.substack.com/p/data-machina-191), nhân một tối đọc và tìm hiểu về prompting. Nếu bạn không ngại đọc tiếng anh, tôi khuyên bạn nên đọc bài viết gốc của tác giả tại link đính kèm ở trên.

### Về Prompt Engineering & GPT Models: Một Chuyến Tham Quan Ngẫu Nhiên. 

Nhiều đồng nghiệp cho rằng prompting và prompt engineering là một "bug của LLMs" và là một "trào lưu sẽ mất đi ngay khi LLMs trở nên tốt hơn", tôi không đồng ý. Prompt engineering còn nhiều hơn chỉ là truy vấn bằng một số từ khóa thông minh. Prompt engineering vẫn sẽ còn tồn tại.

Để lấy nội dung cho bài viết này, tôi rất thích đọc [On Prompt Engineering](https://benjamincongdon.me/blog/2023/02/18/On-Prompt-Engineering/) vì nó truyền đạt nhiều ý tưởng của tôi về chủ đề này.

Prompt engineering đang phát triển nhanh chóng và trở thành một kỹ năng tinh vi. Prompting hơn hết chính là một ngôn ngữ lập trình tự nhiên:

Andrej Karpathy (một học giả về AI rất nổi tiếng, Chief AI of @Tesla) [đã viết trên Twitter](https://twitter.com/karpathy/status/1617979122625712128):

The hottest new programming language is English

(Tạm dịch: Ngôn ngữ lập trình mới nhất nóng hổi là tiếng Anh)

8:14 PM ∙ 24 Tháng 1, 2023

19,412 Lượt thích2,392 Lượt chia sẻ

Trong một webinar gần đây, Chris Potts @StanfordNLP đã nói về old-school prompting và (cutting edge!) prompting từng bước một. Xem trang: [Beyond GPT-3: Các khái niệm chính và câu hỏi mở trong một kỷ nguyên và hiểu biết ngôn ngữ tự nhiên](https://docs.google.com/presentation/d/1WPYaLEEVJJI_-DOzjudeVoYpl_y0yUi1kWs0VFBnba4/edit?usp=sharing).

Prompt engineering đòi hỏi: chuyên môn về lĩnh vực, hiểu cách LLMs phản ứng với các prompt, tư duy có cấu trúc, tư duy giải quyết vấn đề và kỹ năng giao tiếp xuất sắc. Bài luận của Prem rất chính xác: [Prompt Design: Programming with Plain Text, và Prompt Tuning: Learnable Prompts](https://towardsdatascience.com/guiding-a-huge-language-model-lm-to-perform-specific-tasks-prompt-design-and-soft-prompts-7c45ef4794e4).

Một người bạn nói với tôi rằng Anthropic - một startup dẫn đầu trong LLMs - đang gặp khó khăn trong việc tuyển dụng [Kỹ Sư Prompt với mức lương 175.000 đến 335.000 đô la Mỹ mỗi năm](https://jobs.lever.co/Anthropic/e3cde481-d446-460f-b576-93cab67bd1ed), mặc dù đã nhận được hàng trăm đơn xin việc.

Vì vậy, API ChatGPT mới được cung cấp bởi mô hình gpt-turbo-3.5 mới. Bihan @Scale đã viết về [tại sao ChatGPT API nhanh hơn, rẻ hơn và nhiều từ hơn ChatGPT Web UI được cung cấp bởi mô hình text-davinci-003](https://scale.com/blog/chatgpt-vs-davinci#Introduction). Một số khám phá được ghi chép lại trong quá trình kiểm thử. 

Open AI đã đăng tài liệu mới về [một số thay đổi với ChatGPT API và gpt-turbo-3.5](https://platform.openai.com/docs/guides/chat/introduction). Ví dụ: hướng dẫn prompt, hoàn thành trò chuyện, tinh chỉnh tốt hơn và cách sử dụng dữ liệu của bạn.

Bạn có thể thử nghiệm xem các yếu tố prompting đã thay đổi (hoặc chưa) trong các thử nghiệm của mình với mô hình gpt-3.5-turbo mới với [ChatGPT Demo trong Gradio](https://huggingface.co/spaces/anzorq/chatgpt-demo). Nó sử dụng API ChatGPT mới và mẫu lời nhắc từ awesome-chatgpt-prompts.

Hiểu quan hệ giữa các token, prompting và chi phí cũng rất quan trọng khi chạy các mô hình GPT. Để tính toán khoảng 1 triệu token với API ChatGPT mới sẽ tốn... hai đô la... rất rẻ :) !

Một đồng nghiệp nói với tôi rằng có thể chỉ tốn khoảng ~8400 đô la để tạo ra 4,2 tỷ từ của Wikipedia bằng gpt-generate! Tabarak @OpenAI đã viết về: [Token là gì và cách đếm chúng?](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)

Nhưng hãy cẩn thận, bởi sau tốc độ và chi phí tính toán rẻ của API ChatGPT mới, có một sự đánh đổi. Nhiều kỹ sư, startup đã xây dựng ứng dụng sử dụng mô hình text-davinci-003, đã [báo cáo các vấn đề khi chuyển đổi/ tối ưu lại sang gpt-turbo-3.5](https://twitter.com/zachtratar/status/1631429341363212289?s=61&t=ZyNdWIJtgk4tljYelTK-_A).

@baobabKoodaa đã đăng một [notebook về việc chuyển đổi từ davinci-003 sang gpt-3.5-turbo-0301](https://github.com/baobabKoodaa/future/blob/master/server.js#L58-L99) với các hướng dẫn prompting và ví dụ.


