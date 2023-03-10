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

Kỹ thuật viết prompt ngày càng trở nên cầu kì. Không giống như cách bạn viết ngôn ngữ lập trình cho máy hiểu, mà bạn viết như cách cho bộ não con người. Khi viết prompt, người viết cần có kiến thức và hiểu biết về lĩnh vực liên quan đến nội dung mà họ muốn tạo ra prompt. Họ cần biết rõ đối tượng sử dụng prompt và mục đích sử dụng của họ. Ngoài ra, người viết prompt cần có kỹ năng viết văn bản tốt để tạo ra các câu hỏi hoặc yêu cầu có ý nghĩa, đưa ra thông tin cần thiết và tránh những sự hiểu nhầm hoặc mâu thuẫn. Họ cũng cần hiểu các kỹ thuật và công cụ liên quan đến prompting để tạo ra prompt hiệu quả.

Tôi đã đọc nhiều bài trên các trang mạng xã hội. Có nhiều ý kiến thì lo sợ, có nhiều ý kiến thì chê bai. Nhiều người lấy ra các ví dụ khi trò chuyện với ChatGPT về chủ đề chủ thể (mang tính chất chuyên ngành) và họ cho rằng máy học không đưa ra được những câu trả lời họ mong muốn. Tôi thấy một học giả nổi tiếng (trong lĩnh vực KHMT) đăng trên trang cá nhân về ChatGPT chỉ là một mô hình dự đoán dựa trên xác suất, không thể đưa ra những câu trả lời mang tính chất suy diễn, như phép suy luận 'bắc cầu' đơn giản trong toán học. Trong bài viết, tác giả đăng việc hỏi ChatGPT: "Nếu A nặng hơn B, B năng hơn C. Thì A nặng hay nhẹ hơn C?". Chatbot 'ngây thơ' cho rằng: "Mặc dù A nặng hơn B, B năng hơn C nhưng không thể kết luận được A nặng hơn C". Như vậy học giả kết luận ChatGPT không có khả năng của một đứa trẻ mới học toán.

Tuy vậy, câu chuyện không chỉ dừng lại ở đó. Tôi có đọc một vài bình luận phía dưới: một anh tự xưng là kĩ sư nói rằng 🗣️ "trong cơ khí chúng tôi không có đại lượng vật lý thì các phép suy luận không có giá trị". Rồi lấy ví dụ câu hỏi tương tự, chỉ thêm (kg): "Nếu A (kg) nặng hơn B (kg), B (kg) nặng hơn C (kg). Thì A nặng hay nhẹ hơn C?". Ngay lập tức, AI trả lời là A nặng hơn C 😲.

[...]

Để viết được những prompt tốt. Tôi khuyên bạn nên tham khảo thêm các bài giảng tại [promp engineering guide](https://github.com/dair-ai/Prompt-Engineering-Guide)

Ngoài ra cũng có rất nhiều mẫu prompt hay được tổng hợp lại từ cộng đồng trên thế giới. Bạn có thể xem tại [awesome chatgpt prompt](https://github.com/f/awesome-chatgpt-prompts) hoặc học về prompting tại [learn prompting](https://github.com/trigaten/Learn_Prompting).

Trong phần tiếp theo, tôi dịch lại từ trang [Data Machina số #191](https://datamachina.substack.com/p/data-machina-191), nhân một tối đọc và tìm hiểu về prompting. Nếu bạn không ngại đọc tiếng anh, tôi khuyên bạn nên đọc bài viết gốc của tác giả tại link đính kèm ở trên.

### Về Prompt Engineering & GPT Models: Một Chuyến Tham Quan Ngẫu Nhiên. 

Nhiều đồng nghiệp cho rằng prompting và prompt engineering đơn thuần là một "lỗi của mô hình ngôn ngữ" và là một "trào lưu sẽ mất đi ngay khi mô hình ngôn ngữ trở nên tốt hơn", tôi không đồng ý. Prompt engineering không chỉ là truy vấn bằng một số từ khóa thông minh. Prompt engineering vẫn sẽ tiếp tục tồn tại.

Để lấy cảm hứng cho bài viết này, tôi rất thích đọc [On Prompt Engineering](https://benjamincongdon.me/blog/2023/02/18/On-Prompt-Engineering/) vì nó truyền đạt nhiều ý tưởng của tôi về chủ đề này.

Prompt engineering đang phát triển nhanh chóng và trở thành một kỹ năng tinh vi. Prompting hơn hết chính là một ngôn ngữ lập trình tự nhiên:

Andrej Karpathy (một học giả về AI rất nổi tiếng, Chief AI of @Tesla) [đã viết trên Twitter](https://twitter.com/karpathy/status/1617979122625712128) ngày 24 Tháng 1, 2023:

The hottest new programming language is English

(Tạm dịch: Ngôn ngữ lập trình mới nhất nóng hổi là tiếng Anh)

19,412 Lượt thích2,392 Lượt chia sẻ

(Karpathy không gần ngại khi chia sẻ quan điểm, ông không dùng 'will' mà khẳng định rằng nó đã và đang là một ngôn ngữ lập trình nóng hổi)

Trong một webinar gần đây, Chris Potts @StanfordNLP đã nói về old-school prompting và (cutting edge!) prompting, tức là cách tư duy viết prompt cũ và mới. Xem trang: [Beyond GPT-3: Các khái niệm chính và câu hỏi mở trong một kỷ nguyên và hiểu biết ngôn ngữ tự nhiên](https://docs.google.com/presentation/d/1WPYaLEEVJJI_-DOzjudeVoYpl_y0yUi1kWs0VFBnba4/edit?usp=sharing).

Prompt engineering đòi hỏi: chuyên môn về lĩnh vực, hiểu cách LLMs phản ứng với các prompt, tư duy có cấu trúc, tư duy giải quyết vấn đề và kỹ năng giao tiếp xuất sắc. Bài luận của Prem rất chính xác: [Prompt Design: Programming with Plain Text, và Prompt Tuning: Learnable Prompts](https://towardsdatascience.com/guiding-a-huge-language-model-lm-to-perform-specific-tasks-prompt-design-and-soft-prompts-7c45ef4794e4).

Một người bạn nói với tôi rằng Anthropic - một startup dẫn đầu trong LLMs - đang gặp khó khăn trong việc tuyển dụng [Kỹ Sư Prompt với mức lương 175.000 đến 335.000 đô la Mỹ mỗi năm](https://jobs.lever.co/Anthropic/e3cde481-d446-460f-b576-93cab67bd1ed), mặc dù đã nhận được hàng trăm đơn xin việc.

Vì vậy, API ChatGPT mới được cung cấp bởi mô hình gpt-turbo-3.5 mới. Bihan @Scale đã viết về [tại sao ChatGPT API nhanh hơn, rẻ hơn và nhiều từ hơn ChatGPT Web UI được cung cấp bởi mô hình text-davinci-003](https://scale.com/blog/chatgpt-vs-davinci#Introduction). Một số khám phá cũng được ghi chép lại trong quá trình kiểm thử. 

Open AI đã đăng tài liệu mới về [một số thay đổi với ChatGPT API và gpt-turbo-3.5](https://platform.openai.com/docs/guides/chat/introduction). Ví dụ: hướng dẫn prompt, hoàn thành trò chuyện, tinh chỉnh tốt hơn và cách sử dụng dữ liệu của bạn.

Bạn có thể thử nghiệm xem các yếu tố prompting đã thay đổi (hoặc chưa) trong các thử nghiệm của mình với mô hình gpt-3.5-turbo mới với [ChatGPT Demo trong Gradio](https://huggingface.co/spaces/anzorq/chatgpt-demo). Nó sử dụng API ChatGPT mới và mẫu lời nhắc từ awesome-chatgpt-prompts.

Hiểu quan hệ giữa các token, prompting và chi phí cũng rất quan trọng khi chạy các mô hình GPT. Để tính toán khoảng 1 triệu token với API ChatGPT mới sẽ tốn... 2 $... rất rẻ :) !

Một đồng nghiệp nói với tôi rằng có thể chỉ tốn khoảng ~8,4k $ để tạo ra 4,2 tỷ từ của Wikipedia bằng gpt-generate! Tabarak @OpenAI đã viết về: [Token là gì và cách đếm chúng?](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them)

Nhưng hãy cẩn thận, bởi sau tốc độ và chi phí tính toán rẻ của API ChatGPT mới, có một sự đánh đổi. Nhiều kỹ sư, startup đã xây dựng ứng dụng sử dụng mô hình text-davinci-003, đã [báo cáo các vấn đề khi chuyển đổi/ tối ưu lại sang gpt-turbo-3.5](https://twitter.com/zachtratar/status/1631429341363212289?s=61&t=ZyNdWIJtgk4tljYelTK-_A).

@baobabKoodaa đã đăng một [notebook về việc chuyển đổi từ davinci-003 sang gpt-3.5-turbo-0301](https://github.com/baobabKoodaa/future/blob/master/server.js#L58-L99) với các hướng dẫn prompting và ví dụ.

Trong diễn biến khác, Han - tác giả của [PromptPerfect](https://promptperfect.jina.ai/) - anh ấy xác nhận rằng việc chuyển đổi từ davinci003 sang gpt3.5-turbo trong [một vài trường hợp còn sinh ra kết quả tệ hơn](https://twitter.com/hxiao/status/1631333580977721345?s=61&t=iW4mWDdqmuWgaUpuM_71yA).

Điều tra tất cả vấn đề trên chỉ ra rằng, để sinh ra mô hình ngôn ngữ nhanh hơn và rẻ hơn, điều cần làm là sử dụng [LLM distillation và model compression (nén mô hình)](https://quillbot.com/blog/compressing-large-language-generation-models-with-sequence-level-knowledge-distillation/)

Những nghiên cứu sách cũng chỉ ra rằng: các nhà phát triển ứng dụng AI đang điều chỉnh các tham số cho mô hình gpt-3.5-turbo như: temperature, top p, penalty ... Bạn có thể tham khảo cách điều chỉnh này tại [Interactive guide to GPT-3 prompt parameters](https://sevazhidkov.com/interactive-guide-to-gpt-3-prompt-parameters).

Prompting, SQL và phân tích dữ liệu. SQL được cho là ngôn ngữ được sử dụng nhiều nhất trong phân tích dữ liệu. Nếu bạn là người mới vào nghề hoặc đang ở vị trí middle thì bạn nên biết rằng các công ty đang thử nghiệm tự động quá trình truy xuất dữ liệu nhiều hơn bạn nghĩ.

Bạn đã từng thử GPT/Codex cho việc chạy các truy vấn SQL? Đây là một bài báo thú vị về cách cài đặt một môi trường [GPT-SQL để tạo ra sản phẩm chuyển từ ngôn ngữ tự nhiên sang SQL](https://innerjoin.bit.io/making-a-production-llm-prompt-for-text-to-sql-translation-b798b6e94783).

Ngày càng có nhiều công cụ để tạo và quản lý prompt:  Everyprompt, Promptify, OpenPrompt, Betterprompt, Soaked, Dyno... Sau đây là các công cụ khác:
+ Quản lý prompt dễ dàng với [Promptly](https://trypromptly.com/)
+ Khám phá, học và thử nghiệm các ChatGPT prompt với [Prompt Vibes](https://www.promptvibes.com/)
+ [PromptGym](https://github.com/inspired-cognition/critique-apps), vừa thử, đánh giá các prompt khác nhau ở nhiều khía cạnh












