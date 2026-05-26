# alacritty

Установил темы ручками следующим образом

```bash
cd ~/.config/alacritty/
git clone https://github.com/alacritty/alacritty-theme ./themes
```

Напишем конфиг `base_config.toml` с нашими настройками:

```toml
[window]
opacity = 0.96
startup_mode = "Maximized"
# у терминала можно отключить оформление, что может пригодиться любителям тайлинга
# decorations = "None"
dynamic_title = true

# Изменяем курсор
[cursor.style]
shape = "Beam"
blinking = "Always"

[font]
size = 11

# Для лучшей поддержи прозрачности в vim и тп
[colors]
transparent_background_colors = true

[terminal]
shell = {
  program = "/home/vpert/.cargo/bin/zellij",
  args = [
    "attach",
    "--index",
    "0"
  ]
}
```

Напишем простейший скрипт `update_theme.sh`, чтобы менять темы:
```bash
#!/bin/bash
CONFIG_DIR="$HOME/.config/alacritty"
BASE_CONFIG="$CONFIG_DIR/base_config.toml"
THEME_FILE="$CONFIG_DIR/themes/themes/$1.toml"
TARGET_CONFIG="$CONFIG_DIR/alacritty.toml"

if [[ ! -f "$THEME_FILE" ]]; then
    echo "theme $1 not found!"
    exit 1
fi

cat "$BASE_CONFIG" > "$TARGET_CONFIG"

echo "" >> "$TARGET_CONFIG"

cat "$THEME_FILE" >> "$TARGET_CONFIG"

echo "updated config: $TARGET_CONFIG"
```

Закончим с выбором темы:
```bash
chmod +x update_theme.sh
./update_theme.sh aura
```

На этом всё.
