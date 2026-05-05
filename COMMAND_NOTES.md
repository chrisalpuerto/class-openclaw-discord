
# kill gateway
pkill -f openclaw

# start gateway
npx openclaw gateway stop / start

# configure if needed
npx openclaw configure

# start bot
npm run start

(npm install if needed)