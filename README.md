import pygame
import random

# 初始化pygame
pygame.init()

# 设置屏幕大小和标题
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("雪花特效")

# 创建一个空白的surface对象
background = pygame.Surface(screen.get_size())
background.fill((255, 255, 255))

# 定义雪花的属性
snowflakes = []
for i in range(50):
    x = random.randrange(0, 800)
    y = random.randrange(0, 600)
    speed = random.randint(1, 5)
    snowflakes.append([x, y, speed])

# 循环渲染屏幕
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # 在背景上绘制雪花
    for i in range(len(snowflakes)):
        pygame.draw.circle(background, (255, 255, 255), snowflakes[i][:2], snowflakes[i][2])
        snowflakes[i][1] += snowflakes[i][2]
        if snowflakes[i][1] > 600:
            snowflakes[i][1] = random.randrange(-50, -10)
            snowflakes[i][0] = random.randrange(0, 800)

    # 将背景surface对象绘制到屏幕上
    screen.blit(background, (0, 0))

    # 更新屏幕
    pygame.display.flip()

# 退出pygame
pygame.quit()
