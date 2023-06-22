This project analyzes the nutritional value of the popular restaurant, McDonalds. Roy Kroc, the former CEO of Mcdonalds was an American business man with the dream of creating a fast food restaurant with consistent high quality food. This dataset provides a nutrition analysis of every menu item on the US McDonald's menu, including breakfast, beef burgers, chicken and fish sandwiches, fries, salads, soda, coffee and tea, milkshakes, and desserts. The menu items and nutritional facts were scraped from the McDonald's website.
The McDonald's restaurant has 9 categories in their menu of 260 different items and they are:
Coffee & Tea Breakfast Smoothies & Shakes Chicken & Fish Beverages Beef & Pork Snacks & Sides Desserts Salads Most of McDonald's menu fall under the Coffee and Tea category. The category with the least amount of items is Salads with only 6 items in the Menu.

Dự án này phân tích giá trị dinh dưỡng của nhà hàng nổi tiếng McDonalds. Roy Kroc, cựu CEO của Mcdonalds là một doanh nhân người Mỹ với ước mơ tạo ra một nhà hàng thức ăn nhanh với những món ăn chất lượng cao nhất quán. Bộ dữ liệu này cung cấp phân tích dinh dưỡng của mọi món trong thực đơn của McDonald's Hoa Kỳ, bao gồm bữa sáng, bánh mì kẹp thịt bò, bánh mì kẹp thịt gà và cá, khoai tây chiên, sa lát, soda, cà phê và trà, sữa lắc và món tráng miệng. Các món trong thực đơn và thành phần dinh dưỡng đã được lấy từ trang web của McDonald's.
# Set up Data
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import seaborn as sns
    data = pd.read_csv("d:\Mc Donald's  Dataset\menu.csv")
![image](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/2af8b22f-1f22-4082-b3ab-cda76245f618)
# Number Of Menu Items For Each Food Category
     plt.figure()
    menu_category = data.Category.value_counts()
    menu_category.plot.bar(color = ['red','pink','pink','pink','pink','pink','pink','pink','pink'])
    plt.title("Number of Menu Items for each Food Category")
    plt.ylabel("Count")
    plt.xlabel("Menu Category")
    plt.xticks(rotation=45)
    plt.show()
![be1454fe-0e66-4255-b7cf-2ff75d457a3b](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/cb515f2f-d8bd-4b7f-9c37-04d78bc51fa6)
# Fats and Carbohydrates
According to the Harvard School of Public Health, instead of promoting foods with low at in calories. It is important to note that healthy fats are not only beneficial but necessary for health. Generally, there is no relationship between the percentage of calories from fat and major health hazard. Fats can be categorized into three:

Unsaturated Fats. These cateory of fats are good for the health and have a lower disease risk. E.g. Vegetable Oil, Fish, Nuts, Seeds etc.

Trans Fats These are bad fats and increase disease risk even when consumed in small quantities

Saturated Fats These are not as harmful as Trans fat bt can be harmful if not taken in moderation. The Dietary Guidlines for America indicates that saturated fat should not be more than 10% of daily calories and the AMA (American Health Association) recommends aiming for a dietary pattern that achieves 5% to 6% of calories from saturated fats.

Theo Trường Y tế Công cộng Harvard, thay vì quảng cáo thực phẩm ít calo. Điều quan trọng cần lưu ý là chất béo lành mạnh không chỉ có lợi mà còn cần thiết cho sức khỏe. Nói chung, không có mối quan hệ nào giữa tỷ lệ phần trăm calo từ chất béo và mối nguy hiểm lớn đối với sức khỏe. Chất béo có thể được phân loại thành ba:

Chất béo không bão hòa. Nhóm chất béo này tốt cho sức khỏe và ít nguy cơ mắc bệnh. Ví dụ. Dầu thực vật, cá, quả hạch, hạt, v.v.

Chất béo chuyển hóa Đây là những chất béo xấu và làm tăng nguy cơ mắc bệnh ngay cả khi tiêu thụ với số lượng nhỏ

Chất béo bão hòa Đây không phải là chất béo có hại như Chất béo chuyển hóa bt có thể gây hại nếu không dùng điều độ. Hướng dẫn chế độ ăn uống cho người Mỹ chỉ ra rằng chất béo bão hòa không được nhiều hơn 10% lượng calo hàng ngày và AMA (Hiệp hội Y tế Hoa Kỳ) khuyến nghị hướng tới một chế độ ăn kiêng đạt được 5% đến 6% lượng calo từ chất béo bão hòa.

    plt.figure()
    correlation = data["Calories"].corr(data['Calories from Fat'])
    plt.scatter(data.Calories, data["Calories from Fat"],color = 'black')
    plt.text(500,450, 'r ={}'.format(round(correlation,2)))
    plt.xlabel("Calories")
    plt.ylabel("Calories from Fat")
    plt.title("Relationship Calories and Calories from Fat")
    plt.show()
 ![eea34661-57da-4e9a-a8b9-9700c0bcffa8](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/92509dd0-6603-4a0c-a06c-2c183b703ba0)

Giá trị của hệ số tương quan Pearson nằm trong khoảng từ -1 đến 1. Trong trường hợp này, giá trị r = 0.9 cho thấy có một mối tương quan mạnh dương (positive correlation) giữa "Calories" và "Calories from Fat

    data.groupby('Category')['Trans Fat'].mean() 
 Category
Beef & Pork           1.100000

Beverages             0.000000

Breakfast             0.107143

Chicken & Fish        0.129630

Coffee & Tea          0.142105

Desserts              0.000000

Salads                0.000000

Smoothies & Shakes    0.535714

Snacks & Sides        0.000000

Name: Trans Fat, dtype: float64

# Top 5 Food Categories with the highest % Saturated Fat
      data['Saturated_cholesterol'] = round(data['Saturated Fat']/data["Cholesterol"]*100,2)
      data['Saturated_cholesterol']
      saturated_cholesterol = data.groupby('Category')['Saturated_cholesterol'].mean().dropna().nlargest()
      plt.figure()
      saturated_cholesterol.sort_values(ascending=False).plot.bar(color = 'blue')
      plt.title("Top 5 food categories with the highest % Saturated Fat")
      plt.ylabel("Percentage")
      plt.xlabel("Menu Category")
      plt.xticks(rotation=45)
      plt.show()
![4fc3ccbe-c577-4b18-92cf-c03c09679b9b](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/058b7ee3-118e-471a-9d2f-5226d12a335c)

      shakes = data[data.Category =='Smoothies & Shakes']
      shakes.groupby('Item')['Saturated_cholesterol'].mean().sort_values()
![image](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/25161232-9b58-49e7-b590-2ddfb2499581)

      beef_pork = data[data.Category =="Beef & Pork"]
      beef_pork.groupby("Item")["Saturated_cholesterol"].mean().sort_values()
 ![image](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/0760c361-aefd-4691-8079-13b3758f636e)

      chicken_fish = data[data.Category == 'Chicken & Fish']
      chicken_fish.groupby('Item')['Saturated_cholesterol'].mean().sort_values()
 ![image](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/6ff67823-ab21-4e21-af22-c93a194f9fe3)

      data.groupby('Category')['Carbohydrates (% Daily Value)'].mean().sort_values()
 ![image](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/062d125e-2531-4521-bb17-20e40bd1535d)
      plt.figure()
      plt.scatter(data['Total Fat (% Daily Value)'], data['Carbohydrates (% Daily Value)'], color='k')
      correlation = data['Total Fat (% Daily Value)'].corr(data['Carbohydrates (% Daily Value)'])
      plt.text(125,20,'r = {}'.format(round(correlation,2)))
      plt.xlabel("% Total Fat")
      plt.ylabel("% Total Carbohydrate")
      plt.title("Relationship between % Total Fat and % Total Carbohydrate")
      plt.show()
![5db55f7c-cacf-4b71-8991-cd275f5736c8](https://github.com/IamQuangg/Nutritionalfacts/assets/128073066/2acba6f8-6262-4902-b00d-98f1f72b1180) 

There is a strong relationship between Calories and Calories with fat. Hence, food items with high caloric content tend to also have a high calories with fat content.

Generally, McDonalds foods have low trans fat which is good.

The Smoothies and Shakes Menu Category had the highest saturated fat content. Upon analysis, it was discovered that while Fruit shakes had no saturated fat. However, milk Shakes, Chocolate Shakes, Shamrock and McFlurry shakes had high saturated fat with McFlurry at the top of the list.
