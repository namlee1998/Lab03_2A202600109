# Individual Report: Lab 3 - Chatbot vs ReAct Agent

- **Student Name**: LÊ TÚ NAM
- **Student ID**: 2A202600109
- **Date**: 6/4/2026

---

## I. Technical Contribution (15 Points)

*Describe your specific contribution to the codebase (e.g., implemented a specific tool, fixed the parser, etc.).*

- **Modules Implementated**: chatbot and fix bug
- **Code Highlights**: 
*Chatbot code:
def chat(user_input):
    conversation_history.append({"role": "user", "content": user_input})

    response = client.chat.completions.create(
        model=MODEL,
        messages=conversation_history,
    )

    reply = response.choices[0].message.content
    conversation_history.append({"role": "assistant", "content": reply})
    return reply
*Fix bug: 
from datetime import datetime
current_date = datetime.now().strftime("%A, %d/%m/%Y")
-Fix in System prompt:
Current date: {current_date} 

- **Documentation**:Code của em thể hiện rõ rằng LLM giỏi về kể chuyện hơn là xử lý các bước. 
Ngoài ra việc fix bug về vấn đề trả về sai về mặt thời gian khiến cho agent trả về chính xác về mặt thời gian.

## II. Debugging Case Study (10 Points)

*Analyze a specific failure event you encountered during the lab using the logging system.*

- **Problem Description**: Agent trả về thông tin sai về mặt thời gian
- **Log Source**: 
web_search["giá vé xe từ Sài Gòn đi Đà Lạt 2023"]  → No results found.
web_search["giá vé xe khách từ Sài Gòn đi Đà Lạt 2023"] → No results found.
- **Diagnosis**: Vấn đề là do tách tool gọi thời gian ra riêng nên LLM đưa ra câu trả lời dựa trên thông tin từ lần cuối cùng cập nhật
- **Solution**: Update = cách thêm phần "current date".

---

## III. Personal Insights: Chatbot vs ReAct (10 Points)

*Reflect on the reasoning capability difference.*

1.  **Reasoning**: Block Thought giúp cho người dùng dễ dàng debug và biết được agent trả về cái gì.
2.  **Reliability**: Khi gặp những bài toàn đơn giản, agent phải khải qua nhiều vòng lặp nên gây tốn tài nguyên
3.  **Observation**: Nó cập nhật lại suy luận và đưa ra quyết định có gọi vòng lặp tiếp theo không hay đã đủ thông tin để đưa ra quyết định cuối cùng

---

## IV. Future Improvements (5 Points)

*How would you scale this for a production-level AI agent system?*

- **Scalability**: Áp dụng rate limiting + load balancing để đảm bảo hệ thống ổn định khi traffic tăng
- **Safety**: Thêm rule-based guardrails
- **Performance**: Cache kết quả tool call để giảm số lần gọi API lặp lại

---

> [!NOTE]
> Submit this report by renaming it to `REPORT_[YOUR_NAME].md` and placing it in this folder.
