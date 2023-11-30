# macOS setup

## First Step

`xcode-select --install`

## oh-my-zsh install
* Check if it's installed
* Install if it's not

```zsh
if [ -d "$ZSH" ]; then
  e_warning "Oh My Zsh is already installed. Skipping.."
else
  e_header "Installing Oh My Zsh..."
  curl -L http://install.ohmyz.sh | sh
  ## install ZSH plugins
  #Z
  e_header "Installing ZSH Plugins"
  git clone https://github.com/MichaelAquilina/zsh-you-should-use.git $ZSH_CUSTOM/plugins/you-should-use
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
  ## To install ZSH themes & aliases
  e_header "Copying ZSH themes & aliases..."
  e_note "Check .aliases file for more details."
  ln -sf oh-my-zsh/aliases ~/.aliases                                        ## Copy aliases
  ln -sf oh-my-zsh/zshrc ~/.zshrc                                            ## Copy zshrc configs
fi
```

## Brew Install
* Check for install 
* install if it's not installed

```zsh
if test ! $(which brew); then
  e_header "Installing Homebrew"
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
else
  e_warning "Homebrew is already installed. Skipping.."
fi
```

## NVM/Node install

```zsh
if test ! $(which nvm); then
  e_header "Installing zsh-nvm.."

  git clone https://github.com/lukechilds/zsh-nvm $ZSH_CUSTOM/plugins/zsh-nvm

  ## To setup npm install/update -g without sudo
  ln -sf  npmrc ~/.npmrc
  mkdir "${HOME}/.npm-packages"
  export PATH="$HOME/.node/bin:$PATH"
  sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}

  ## Set npm global config
  npm config set init.author.name "Dan Cigrang" ## Replace it with your name
  npm config set init.author.email "danielcigrang@me.com" ## Replace it with your email id
else
  e_warning "NVM is already installed. Skipping.."
fi
```