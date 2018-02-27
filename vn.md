# Cách nào để viết CSS có thể mở rộng và bảo trì? Đây chính là điều mà mỗi front-end developer đều băn khoăn. ITCSS có câu trả lời?

Năm ngoái, khi chúng tôi bắt đầu thưc hiện kế hoạch thiết kế lại [HEROized](http://www.heroized.com) và tạo thiết kế mới cho website Xfive.co, tôi đã tìm kiếm kiến trúc CSS cho phép dễ dàng phát triển và bảo trì sau này.

[CSS Modules](https://www.sitepoint.com/understanding-css-modules-methodology/) khá là mới và lạ lẫm vào thời điểm đó và tôi luôn
cân nhắc (PHÂN VÂN)... Sau đó tôi có đọc bài viết ITCSS của [Harry Roberts](https://csswizardry.com/) trên [báo mạng](https://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731).
được phát hành hôm 6/2015. Và ngay lập tức tôi đã bị thuyết phục với cách tiếp cận CSS đơn giản từ dưới nên trên này.
 
## ITCSS là gì?

ITCSS viết tắt của `Inverted Triangle CSS` và nó giúp bạn có thể tổ chức các file CSS trong project của mình
theo cách nào đó để có thể **giải quyết các vấn đề** (không phải tất cả đêu giải quyết được) với CSS cụ thể như **các thuộc tính global namespace, cascade, và các selector.**
 
ITCSS có thể được dùng mà không bắt buộc cần có các bộ tiền xử lý và nó cũng tương thích với các cách logic để viết CSS như BEM, SMACSS hay OOCSS.

Một trong những nguyên tắc chính của ITCSS là nó tách codebase thành các thành phần khác nhau riêng lẻ(được gọi là các `layer`), nó có hình dạng của một tam giác ngược: 

![img](https://www.xfivecdn.com/xfive/wp-content/uploads/2016/02/01083650/itcss-layers2.svg)

Các layer:

* **Settings** – sử dụng cùng với bộ tiền xử lý và nó bao gồm các khai báo font, colors, ...
* **Tools** – các function và các mixin được sử dụng trong phạm vi global. Lưu ý quan trọng là không viết bất kỳ CSS vào 2 layer đầu tiên này.
* **Generic** – reset và/hoặc định nghĩa các style, box-sizing,...Đây là tầng đầu tiên tạo ra CSS thực sự.
* **Elements** – xét style cho các thẻ HTML thuần (H1, A,...). Các thẻ này sử dụng style mặc định của browser nên ta có thể định nghĩa lại chúng trong layer này.
* **Objects** – các selector class định nghĩa các thành phần mẫu chưa được thiết kế, ví dụ: media object của OOCSS
* **Components** – các thành phần UI riêng biệt. Đây là nơi ta sẽ thao tác, làm việc nhiều nhất và các UI components thường được tạo từ các Object và các component khác. 
* **Utilities** – chứa các helper class và các ulitiles class có thể ghi đè bởi bất kỳ thành thành phần nào được khai báo trước trong tam giác, ví dụ ẩn helper class.
 
Tam giác này cũng thể hiện các style mà các selector quy định ...: từ cái chung đến cái riêng, từ các selector có chỉ định mức độ cụ thể style thấp đến các
selector chỉ định mức độ cụ thể hơn (nhưng không quá cụ thể, ID không được phép) và từ thành phần dùng mang tính tổng quát cao đến các thành phần cụ thể trong các trường hợp. 

![img2](https://www.xfivecdn.com/xfive/wp-content/uploads/2016/02/10154630/itcss-key-metrics.svg)

Việc tổ chức code CSS giúp bạn có thể tránh được các xung đột và được thể hiện rõ trong [đồ thị đặc trưng](https://jonassebastianohlsson.com/specificity-graph).

## Tài liệu

Cập nhật ngày 27/10/2016: tờ báo đã phát hành lại bài viết ban đầu trên báo in.

Theo thường lê, tôi sẽ giới thiệu tới bạn website [ITCSS webpage](https://itcss.io) để tìm hiểu thêm. Tuy nhiên, nó không có bất kỳ thứ gì cả, kể cả tài liệu tham khảo.

ITCSS thuộc sở hữu độc quyền nếu bạn muốn sử dụng toàn bộ nó thì bạn nên đọc phần giới thiệu trong tạp chí. Tôi không ở đây để bàn luận về mục đích
của tác giả bài viết (tôi biết ơn vì anh ấy đã chia sẻ kiến thức của mình), nhưng theo tôi nghĩ điều đó để hạn chế việc ITCSS bị áp dụng rộng rãi (đó có thể là mục đích chính).

```
" Tính độc quyền của ITCSS hạn chế việc nó được áp dụng rộng rãi
```

Điều đó không ngăn cản việc bạn bắt đầu sự dụng nó trong project của mình, nếu thich thú hãy làm nó ngay. [Truy cập bài viết](https://www.myfavouritemagazines.co.uk/design/net-magazine-back-issues/)
để tìm hiểu các nguyên tắc cơ bản của ITCSS và sau đó nghiên cứu các ví dụ, tài liệu online để giúp bạn áp dụng nó vào trong project thực tế.

## Nguồn tài nguyên

Tôi đã sử dụng ITCSS trong 4 project và cả những cái sau này nữa (bao gồm cả Xfive.co). Dưới đây là các nguồn tài liệu giúp tôi hiểu rõ hơn về ITCSS:

- [Manage large CSS projects with ITCSS](http://www.creativebloq.com/web-design/manage-large-css-projects-itcss-101517528) – ITCSS giới thiệu bởi Harry Roberts (bài viết ban đầu đã được xuất bản trên báo giấy, thiếu các cột shorters trong đồ thị đặc tính và tiền chỉ thị)
- [Manage large-scale web projects with new CSS architecture ITCSS](http://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731) –  giới thiệu về ITCSS và phỏng vấn Harry Roberts
- [Harry Roberts – Managing CSS Projects with ITCSS](https://www.youtube.com/watch?v=1OKZOV-iLj4) – cuộc nói chuyện của Harray tạ DaFED và slide đi kèm. 
- [Manage large CSS projects with ITCSS](https://www.youtube.com/watch?v=hz76JIU_xB0) – hình chụp trên bài viết trên mạng.
- [ITCSS Screencast code](https://github.com/itcss/itcss-netmag) – code của những screencast bên trên trên GitHub.
- [Another ITCSS project example](https://github.com/csswizardry/frcss)
- Các bài viết trên csswizardry.com liệt kê dưới đây:
    - [BEMIT: Taking the BEM Naming Convention a Step Further](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)
    - [More Transparent UI Code with Namespaces](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
    - [Immutable CSS](https://csswizardry.com/2015/03/immutable-css/)
    - [The Specificity Graph](https://csswizardry.com/2014/10/the-specificity-graph/)
- [inuitcss](https://github.com/inuitcss/inuitcss) – Framework 00CSS xây dụng dựa vào ITCSS và nó đưa ra nhiều khái niệm và các tính năng nâng cao hơn.
- [The BEMIT naming convention](http://www.jamesturneronline.net/blog/bemit-naming-convention.html)

Bạn có thể theo dõi[Chisel](https://github.com/xfiveco/generator-chisel/), nhà sáng lập ra Yeoman cho các dự án front-end của WordPress, nó có hỗ trợ ITCSS.

##Trải nghiệm

Đây là một vài cảm nhân dựa trên trải nghiệm của tôi về project ITCSS

### Bớt đắn đo về việc đặt tên và vị trí thiết lập các style

ITCSS có tính nhất quán và đặc biệt khi sử dụng nó với [BEMIT naming convention](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)
cho phép bạn tập trung hơn vào việc giải quyết các vấn đề front-end hơn là luôn phải nghĩ cách đặt tên và vị trí các style. Đây là file main.scss của Xfile.co:

    @import "settings.colors";
    @import "settings.global";
    
    @import "tools.mixins";
    
    @import "normalize-scss/normalize.scss";
    @import "generic.reset";
    @import "generic.box-sizing";
    @import "generic.shared";
    
    @import "elements.headings";
    @import "elements.hr";
    @import "elements.forms";
    @import "elements.links";
    @import "elements.lists";
    @import "elements.page";
    @import "elements.quotes";
    @import "elements.tables";
    
    @import "objects.animations";
    @import "objects.drawer";
    @import "objects.list-bare";
    @import "objects.media";
    @import "objects.layout";
    @import "objects.overlays";
    
    @import "components.404";
    @import "components.about";
    @import "components.archive";
    @import "components.avatars";
    @import "components.blog-post";
    @import "components.buttons";
    @import "components.callout";
    @import "components.clients";
    @import "components.comments";
    @import "components.contact";
    @import "components.cta";
    @import "components.faq";
    @import "components.features";
    @import "components.footer";
    @import "components.forms";
    @import "components.header";
    @import "components.headings";
    @import "components.hero";
    @import "components.jobs";
    @import "components.legal-nav";
    @import "components.main-cta";
    @import "components.main-nav";
    @import "components.newsletter";
    @import "components.page-title";
    @import "components.pagination";
    @import "components.post-teaser";
    @import "components.process";
    @import "components.quote-banner";
    @import "components.offices";
    @import "components.sec-nav";
    @import "components.services";
    @import "components.share-buttons";
    @import "components.social-media";
    @import "components.team";
    @import "components.testimonials";
    @import "components.topbar";
    @import "components.reasons";
    @import "components.wordpress";
    @import "components.work-list";
    @import "components.work-detail";
    
    @import "vendor.prism";
    
    @import "trumps.clearfix";
    @import "trumps.utilities";
    
    @import "healthcheck";
    
Lưu ý: chúng tôi sử dụng các [folder riêng biệt cho từng layer](https://github.com/xfiveco/generator-chisel/tree/master/generators/app/templates/styles/itcss)
và nạp stylesheets được thêm mới một cách tự động trong [Chisel](https://github.com/xfiveco/generator-chisel/).

### Các object có khả năng tái sử dụng cho việc phát triển nhanh chóng

Các object của ITCSS là đối tượng hoàn hảo để xây dựng thư viện chứa các component có thể tái sử dụng cho phép xây dụng front-end nhanh chóng.
Các thành phần UI khi đó sẽ bao gồm các object dùng chung và các componet cụ thể trong project. Ví dụ, (innuitcss) như là một frameworm dựa trên ITCSS, nó bao gồm [tập hợp các đối tượng](https://github.com/inuitcss/inuitcss/tree/develop/objects) nhưng chỉ là [một component mẫu](https://github.com/inuitcss/inuitcss/tree/develop/components)

### Hiệu ứng

Tôi khuyến khích nên khai báo các hiệu ứng dùng chung và toàn cục giống như các object, ví dụ: `@keyframes o-fade-in` viết trong file `_objects.animations.scss`

Các hiệu ứng cho các component cụ thể nào đó nên được định nghĩa trong các file component tương ứng, ví dụ: `@keyframes c-hero-scale` khai báo trong `_components.hero.scss`


### Tính linh hoạt

ITCSS khá là linh hoạt trong các công cụ và workflow của bạn. Một developers của chúng tôi đã từng thắc mắc có bao nhiêu bản mẫu đi kèm với ITCSS. Nhưng thực tế điều này hoàn toàn tùy thuộc vào bạn, ITCSS không bắt buộc bạn phải có tất cả các thể hiện của layer(chỉ là cần đúng thứ tự).    

Vì thể trong một thiết lập tối thiểu, bạn có thể chỉ có các component được gán style mặc định bởi browser. Tất nhiên, như thể không có tính thực tế - một vài thiết lập, reset và/hoặc CSS thông thường được hầu hết mọi người sử dụng vì những lý do tốt.

### Không hài lòng

ITCSS làm tốt với CSS là nhờ tam giác ngược. Component dựa trên model cho phép bạn tách UI trên giao diện người dùng thành các thành phần logic nên bạn thậm chí có thể lấy các phần của CSS quan trọng bằng tay (chi tiết trong bài viết sắp tới).

### Việc lặp lại style và kích thước của file

Nếu có bất kỳ mối quan tâm với một kiến ​​trúc như ITCSS hoặc về bất kỳ thành phần cơ bản nào như kiến ​​trúc CSS, nó có thể là kích thước tập tin

ITCSS không thể cạnh tranh với [CSS chức năng](https://blog.colepeters.com/building-and-shipping-functional-css/) theo nghĩa này. Hay nói cách khác, nếu bạn thấy mình lặp lại rất nhiều style trong các component, bạn có thể cân nhắc chuyển các style này sang các đối tượng riêng biệt.

### Kết luận

Bạn không thể làm sai với ITCSS. Đó là sự đúc kết của kinh nghiệm và nhiều năm làm việc của Harry Roberts, một trong những tác giả CSS nổi tiếng nhất. Nếu bạn không ngại tìm hiểu sâu vào các resource, bạn sẽ có một kiến ​​trúc đơn giản nhưng mạnh mẽ sẽ cho phép bạn tạo CSS có thể mở rộng và duy trì được cho các dự án nhỏ hoặc lớn của bạn.

Nhưng đùng quên theo dõi các yếu tố khác như [CSS modules](https://github.com/css-modules/css-modules)
But don’t forget to keep an eye on other players like[CSS modules](https://github.com/css-modules/css-modules), in the meantime.


### Nguồn

- [https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)