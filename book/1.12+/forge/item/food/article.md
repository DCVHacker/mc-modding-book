# Создание еды

## Основа

В прошлом уроке вы научились создавать предмет, а теперь давайте создадим еду, чтобы наш персонаж был сыт и мог заморить червячка. Создадим класс для нашей еды, пусть будет кокос.

```java
public class ItemCoconut extends ItemFood
{
    public ItemCoconut(String name, int amount, float saturation, boolean isWolfFood)
    {
        super(amount, saturation, isWolfFood);
        this.setRegistryName(name);
        this.setUnlocalizedName(name);
    }
}
```

Появились новые параметры, такие как `amount`, `saturation`, `isWolfFood`.
* `amount` - отвечает за количество восполняемого голода.
* `saturation` - отвечает за длительность сытости.
* `isWolfFood` - отвечает за то, может ли волк есть нашу еду.

Для еды мы так же можем использовать такой метод:
`this.setAlwaysEdible()` - позволяет есть предмет даже когда шкала голода заполнена.

Добавим переменную в ItemsRegister.
```java
public static Item COCONUT = new ItemCoconut("coconut", 1, 0.5F, false);
```
и зарегистрируем нашу еду по прошлому уроку. Так же не забудьте добавить модель к вашему предмету(см. прошлый урок).

## Добавление эффекта при съедании

Вернёмся к нашему классу еды и добавим туда метод `onFoodEaten`.
```java
@Override
protected void onFoodEaten(ItemStack stack, World worldIn, EntityPlayer player)
{
    super.onFoodEaten(stack, worldIn, player);

    if(player.getFoodStats().getFoodLevel() > 2)
    {
        player.addPotionEffect(new PotionEffect(Potion.getPotionById(9), 100));
    }
}
```
Из кода видно, что если у игрока уровень голода больше 2, то мы добавляем игроку эффект зелья тошноты (id = 9), которое будет длится 5 секунд. 100 / 20 = 5. 20 это тики, в 1 секунде 20 тиков.

Перейдём в игру и попробуем съесть нашу еду.
