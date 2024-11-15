# root

distances = {
    1: [0, 10, 15, 20],
    2: [10, 0, 35, 25],
    3: [15, 35, 0, 30],
    4: [20, 25, 30, 0]
}

bestAnswer = float('inf')
bestPath = ""
cities = [2, 3, 4]

def calcDistance(i, j):
    return distances[i][j - 1]

def tsp(current_city, remaining_cities, current_distance):
    global bestAnswer, bestPath

    # اگر هیچ شهری باقی نمانده باشد، به شهر مبدأ برمی‌گردیم
    if not remaining_cities:
        final_distance = current_distance + calcDistance(current_city, 1)
        if final_distance < bestAnswer:
            bestAnswer = final_distance
            bestPath = f"1 -> {' -> '.join(map(str, path))} -> 1"
        return

    for city in remaining_cities:
        # محاسبه فاصله جدید
        new_distance = current_distance + calcDistance(current_city, city)
        
        # اگر فاصله جدید از بهترین پاسخ بزرگتر باشد، ادامه ندهید
        if new_distance >= bestAnswer:
            continue
        
        # ایجاد لیست جدید از شهرهای باقی‌مانده
        new_remaining_cities = remaining_cities.copy()
        new_remaining_cities.remove(city)
        
        # اضافه کردن شهر فعلی به مسیر
        path.append(city)
        
        # فراخوانی بازگشتی
        tsp(city, new_remaining_cities, new_distance)
        
        # حذف شهر فعلی از مسیر (backtrack)
        path.pop()

# لیست مسیر برای ذخیره کردن ترتیب سفر
path = []

# شروع از شهر 1 و با شهرهای باقی‌مانده
tsp(1, cities, 0)

print(bestAnswer)
print(bestPath)