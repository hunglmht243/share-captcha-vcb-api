Mình share api giải captcha VCB cho ai cần...

Quá trình train model:

1. Xử lí ảnh. 1 số hàm mình dùng:
  + filter2D cùng kernel để tách bớt đường kẻ ngang
  + Affine để kéo ảnh từ nghiêng sang thẳng.
  + morphologyEx cùng adaptiveThreshold để xóa bớt chấm đen gây nhiễu
  + sau cùng là findContours để tách số. trường hợp nhiều hơn 2 chữ dính vào nhau thì mình chia đôi chia ba tùy kích thước chiều rộng ảnh
2. Build model và train thôi:

  + mình tham khảo và custom lại model của MNIST model. sau nhiều lần chỉnh model thì đây là cấu trúc model của mình

  + mình cào tay được hơn 400 ảnh captcha nên dataset có 2000 input. Mình train khoảng 50 epochs cho ra tỉ lệ chính xác là 99%. Và khi dự đoán cả 5 số     của 1 ảnh captcha thì cho ra tỉ lệ chính xác là 94%.
Api document:
Vì model cũng nhẹ nên mình deploy lên aws lambda để lấy 1000000 request free mỗi tháng ✌️

POST  https://m55fcyky7kjygarwkogp5zvix40lqagi.lambda-url.ap-southeast-1.on.aws/

Body raw (json)
  {
      "base64img": "data:image/jpeg;base64,/9j/4AAQSkZJRgA....................."
  }

Nếu mọi người ủng hộ bài sau mình sẽ share cách mình reverse api của VCB để auto lấy transaction history phục vụ các web shop bán hàng

Thắc mắc liên hệ: t.me/dinhhung_243
