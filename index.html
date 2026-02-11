import React, { useState, useEffect, useRef } from 'react';
import { Shield, Sword, ShoppingBag, Heart, Skull, Briefcase, Footprints, LogOut, Zap, AlertTriangle, Radio, Coins, Trash2, Utensils, Smile, EyeOff, Activity, Hammer, HelpCircle, Gem } from 'lucide-react';

// --- 游戏数据配置 ---

const ITEMS = {
  medkit:   { id: 'medkit', name: '急救包', type: 'consumable', cost: 60, effect: 'heal', value: 40, desc: '恢复40生命', rarity: 'white' },
  food:     { id: 'food', name: '压缩饼干', type: 'consumable', cost: 30, effect: 'satiety', value: 40, desc: '恢复40饱食', rarity: 'white' },
  alcohol:  { id: 'alcohol', name: '陈年威士忌', type: 'consumable', cost: 80, effect: 'mood', value: 50, desc: '恢复50心情,减少10San', rarity: 'green' },
  pills:    { id: 'pills', name: '镇静剂', type: 'consumable', cost: 120, effect: 'sanity', value: 40, desc: '恢复40理智(San)', rarity: 'blue' },
  ammo_box: { id: 'ammo_box', name: '自制弹药箱', type: 'consumable', cost: 0, effect: 'buff_atk', value: 10, desc: '下一次战斗伤害+10 (工作台制造)', rarity: 'green' },
};

const GEAR = {
  knife:    { id: 'knife', name: '生锈匕首', type: 'weapon', cost: 0, atk: 2, desc: '聊胜于无' },
  pistol:   { id: 'pistol', name: '旧手枪', type: 'weapon', cost: 150, atk: 5, desc: '可靠的伙伴' },
  rifle:    { id: 'rifle', name: '突击步枪', type: 'weapon', cost: 400, atk: 12, desc: '火力压制' },
  clothes:  { id: 'clothes', name: '便服', type: 'armor', cost: 0, def: 0, desc: '不防弹' },
  vest:     { id: 'vest', name: '防弹背心', type: 'armor', cost: 200, def: 3, desc: '减少3点伤害' },
  heavy:    { id: 'heavy', name: '重型装甲', type: 'armor', cost: 500, def: 8, desc: '移动坦克' },
};

// --- 新增：遗物系统 ---
const RELICS = {
  vampire:    { id: 'vampire', name: '吸血鬼之牙', desc: '击杀敌人回复 5 HP', rarity: 'purple', type: 'relic' },
  cat:        { id: 'cat', name: '招财猫', desc: '撤离结算金币 +20%', rarity: 'purple', type: 'relic' },
  adrenaline: { id: 'adrenaline', name: '肾上腺素', desc: 'HP < 30% 时攻击力翻倍', rarity: 'purple', type: 'relic' },
};

// --- 新增：设施升级配置 ---
const FACILITIES = {
  medical:   { id: 'medical', name: '战地医疗站', cost: { '螺丝组件': 10, '废旧钢材': 5 }, desc: '撤离后自动恢复翻倍 (20->40)' },
  workbench: { id: 'workbench', name: '精密工作台', cost: { '线材组件': 5, '蓄电池': 1 }, desc: '允许消耗废料制造强力弹药' },
  kitchen:   { id: 'kitchen', name: '野战厨房', cost: { '神秘肉罐头': 3 }, desc: '饱食度上限 +50' },
};

// --- 新增：分支事件配置 ---
const STORY_EVENTS = [
  {
    id: 'injured_scavenger',
    text: '你发现一个受伤的拾荒者靠在墙边，腹部的伤口正在渗血。',
    choices: [
      { id: 'help', text: '救助 (消耗急救包)', req: { item: 'medkit' }, resultText: '你包扎了他的伤口。他感激地塞给你一些东西。', mood: 20, sanity: 5, lootChance: 1.0 },
      { id: 'rob', text: '打劫', resultText: '你趁火打劫。他试图反抗...', combat: true, enemyId: 'weak_scavenger', mood: -10, sanity: -10 },
      { id: 'ignore', text: '无视', resultText: '你从他身边走过，假装没听见他的呻吟。', mood: -5, sanity: -2 }
    ]
  },
  {
    id: 'abandoned_shrine',
    text: '废墟深处有一座堆满电子元件的奇怪祭坛，散发着微光。',
    choices: [
      { id: 'pray', text: '祈祷 (消耗5饱食)', req: { stat: 'satiety', val: 5 }, resultText: '你感到一阵平静，但也更加饥饿。', mood: 10, sanity: 20 },
      { id: 'desecrate', text: '搜刮祭坛', resultText: '你拿走了上面的零件，但感觉有什么东西跟上了你...', combat: true, enemyId: 'glitch', mood: 0, sanity: -15, lootChance: 1.0 },
      { id: 'leave', text: '离开', resultText: '不作死就不会死。', mood: 0, sanity: 0 }
    ]
  }
];

// 物品稀有度
const RARITY_CONFIG = {
  white:   { label: '普通', color: 'text-slate-400', border: 'border-slate-500', bg: 'bg-slate-800' },
  green:   { label: '优良', color: 'text-emerald-400', border: 'border-emerald-500', bg: 'bg-emerald-900/20' },
  blue:    { label: '稀有', color: 'text-cyan-400', border: 'border-cyan-500', bg: 'bg-cyan-900/20' },
  purple:  { label: '史诗', color: 'text-fuchsia-400', border: 'border-fuchsia-500', bg: 'bg-fuchsia-900/20' },
  gold:    { label: '传说', color: 'text-amber-400', border: 'border-amber-500', bg: 'bg-amber-900/20' },
  special: { label: '特殊', color: 'text-red-500 animate-pulse', border: 'border-red-500', bg: 'bg-red-900/20' },
};

const LOOT_DB = [
  { name: '螺丝组件', val: 15, rarity: 'white', type: 'loot' },
  { name: '废旧钢材', val: 25, rarity: 'white', type: 'loot' },
  { name: '神秘肉罐头', val: 30, rarity: 'white', type: 'loot' },
  { name: '粗糙布料', val: 50, rarity: 'green', type: 'loot' },
  { name: '线材组件', val: 65, rarity: 'green', type: 'loot' },
  { name: '未知酱料', val: 80, rarity: 'green', type: 'loot' },
  { name: '好用的钳子', val: 150, rarity: 'blue', type: 'loot' },
  { name: '润滑油', val: 180, rarity: 'blue', type: 'loot' },
  { name: '燃气瓶', val: 220, rarity: 'blue', type: 'loot' },
  { name: '优质钢材', val: 400, rarity: 'purple', type: 'loot' },
  { name: '蓄电池', val: 550, rarity: 'purple', type: 'loot' },
  { name: '火药', val: 600, rarity: 'purple', type: 'loot' },
  { name: '求生急救包', val: 1000, rarity: 'gold', type: 'loot' },
  { name: '完整抗生素', val: 1200, rarity: 'gold', type: 'loot' },
  { name: '求生无线电发射器', val: 5000, rarity: 'special', type: 'loot' },
  // 遗物加入掉落池 (低概率)
  { ...RELICS.vampire, val: 800 },
  { ...RELICS.cat, val: 800 },
  { ...RELICS.adrenaline, val: 800 },
];

const ENEMIES = [
  { id: 'rat', name: '变异老鼠', hp: 10, atk: 3, exp: 10 },
  { id: 'scavenger', name: '流浪拾荒者', hp: 25, atk: 6, exp: 30 },
  { id: 'thug', name: '武装暴徒', hp: 45, atk: 10, exp: 60 },
  { id: 'merc', name: '精英佣兵', hp: 80, atk: 15, exp: 150 },
];

// --- 样式组件 ---

const PixelCard = ({ children, className = "", onClick, disabled }) => (
  <div 
    onClick={!disabled ? onClick : undefined}
    className={`
      relative border-2 border-slate-600 bg-slate-800 p-3 
      shadow-[2px_2px_0px_0px_rgba(0,0,0,0.8)] 
      active:shadow-none active:translate-y-[2px] active:translate-x-[2px]
      transition-all cursor-pointer select-none text-slate-200
      ${disabled ? 'opacity-50 cursor-not-allowed grayscale' : 'hover:bg-slate-700 hover:border-slate-400'}
      ${className}
    `}
  >
    {children}
  </div>
);

const ProgressBar = ({ current, max, color = "bg-green-600", label, icon }) => (
  <div className="flex items-center gap-1 text-sm leading-none mb-1 pixel-font w-full">
    {icon && <span className="w-4 text-slate-400">{icon}</span>}
    <div className="flex-1 h-2 bg-slate-900 border border-slate-600 relative">
      <div 
        className={`h-full ${color} transition-all duration-300`} 
        style={{ width: `${Math.max(0, Math.min(100, (current / max) * 100))}%` }}
      />
    </div>
  </div>
);

// --- 主组件 ---

export default function ExtractionGame() {
  const [scene, setScene] = useState('home'); // home, shop, storage, hideout, raid, combat, event, interactive_event, result, gameover
  const [logs, setLogs] = useState(["欢迎来到 0 号禁区。存活，搜刮，暴富。"]);
  
  // 玩家状态
  const [player, setPlayer] = useState({
    hp: 100, maxHp: 100,
    satiety: 100, maxSatiety: 100,
    mood: 100, maxMood: 100,
    sanity: 100, maxSanity: 100,
    money: 200,
    weapon: GEAR.knife,
    armor: GEAR.clothes,
    relics: [],        // 已装备的遗物
    facilities: {},    // 已解锁的设施 { medical: true }
    inventory: [],
    storage: [],       // 仓库
  });

  const [raidState, setRaidState] = useState({
    distance: 0,
    dangerLevel: 1,
    currentEnemy: null,
    isGlitchEnemy: false,
    tempLoot: [],     
    currentLootItem: null,
    currentInteractiveEvent: null, // 当前触发的互动事件
  });

  const addLog = (msg, type = 'neutral') => {
    const time = new Date().toLocaleTimeString('zh-CN', { hour12: false, hour: '2-digit', minute: '2-digit', second: '2-digit' });
    setLogs(prev => [`[${time}] ${msg}`, ...prev].slice(0, 8));
  };

  // --- 辅助函数：检查仓库物品 ---
  const countItemInStorage = (itemName) => {
    return player.storage.filter(i => i.name === itemName).length;
  };

  const removeItemsFromStorage = (itemName, count) => {
    let removed = 0;
    const newStorage = player.storage.filter(item => {
      if (item.name === itemName && removed < count) {
        removed++;
        return false;
      }
      return true;
    });
    return newStorage;
  };

  // --- 核心逻辑：设施升级 ---
  const upgradeFacility = (facId) => {
    const facility = FACILITIES[facId];
    if (player.facilities[facId]) return; // 已升级

    // 检查材料
    let canBuild = true;
    for (const [name, count] of Object.entries(facility.cost)) {
      if (countItemInStorage(name) < count) canBuild = false;
    }

    if (canBuild) {
      let newStorage = [...player.storage];
      for (const [name, count] of Object.entries(facility.cost)) {
        // 简化的批量删除逻辑
        let removed = 0;
        newStorage = newStorage.filter(item => {
          if (item.name === name && removed < count) {
            removed++;
            return false;
          }
          return true;
        });
      }

      const newFacilities = { ...player.facilities, [facId]: true };
      let updates = { storage: newStorage, facilities: newFacilities };

      // 应用即时效果
      if (facId === 'kitchen') {
        updates.maxSatiety = 150;
        updates.satiety = 150;
      }

      setPlayer(prev => ({ ...prev, ...updates }));
      addLog(`设施建造成功：${facility.name}`, 'success');
    } else {
      addLog('材料不足，无法建造！', 'error');
    }
  };

  // --- 核心逻辑：制造弹药 ---
  const craftAmmo = () => {
    // 消耗 1废旧钢材 + 1火药 (简化：消耗$50 + 1废旧钢材)
    const costMoney = 50;
    const material = '废旧钢材';
    
    if (player.money >= costMoney && countItemInStorage(material) >= 1) {
      const newStorage = removeItemsFromStorage(material, 1);
      setPlayer(prev => ({
        ...prev,
        money: prev.money - costMoney,
        storage: [...newStorage, { ...ITEMS.ammo_box, type: 'consumable' }]
      }));
      addLog('制造了 自制弹药箱', 'success');
    } else {
      addLog('制造材料或资金不足 ($50 + 废旧钢材)', 'error');
    }
  };

  // --- 核心逻辑：交互事件选择 ---
  const handleEventChoice = (choice) => {
    // 检查条件
    if (choice.req) {
      if (choice.req.item) {
        const hasItem = player.storage.some(i => i.id === choice.req.item); // 简化：检查仓库/背包
        // 这里为了简化，假设Raid中可以直接消耗“携带”的物品，但目前我们没有做携带逻辑。
        // 我们假设如果仓库有急救包，这次就能用。更严谨的逻辑需要Raid背包。
        // 暂时逻辑：检查storage，消耗storage。
        if (!hasItem) {
          addLog('缺少所需物品！', 'error');
          return;
        }
        // 消耗物品
        const idx = player.storage.findIndex(i => i.id === choice.req.item);
        const newStorage = player.storage.filter((_, i) => i !== idx);
        setPlayer(prev => ({ ...prev, storage: newStorage }));
      }
      if (choice.req.stat) {
        if (player[choice.req.stat] < choice.req.val) {
          addLog('状态不足！', 'error');
          return;
        }
        setPlayer(prev => ({ ...prev, [choice.req.stat]: prev[choice.req.stat] - choice.req.val }));
      }
    }

    // 应用结果
    addLog(choice.resultText);
    
    // 状态变更
    if (choice.mood) setPlayer(prev => ({ ...prev, mood: Math.min(prev.maxMood, prev.mood + choice.mood) }));
    if (choice.sanity) setPlayer(prev => ({ ...prev, sanity: Math.min(prev.maxSanity, prev.sanity + choice.sanity) }));

    // 战斗触发
    if (choice.combat) {
      let enemyTemplate = ENEMIES[0];
      if (choice.enemyId === 'weak_scavenger') enemyTemplate = { name: '受伤的拾荒者', hp: 15, atk: 4, exp: 20 };
      if (choice.enemyId === 'glitch') enemyTemplate = { name: '?%#ERROR', hp: 60, atk: 12, exp: 0 };
      
      setRaidState(prev => ({ ...prev, currentEnemy: { ...enemyTemplate, maxHp: enemyTemplate.hp }, isGlitchEnemy: choice.enemyId === 'glitch' }));
      setScene('combat');
      return; // 结束，进入战斗
    }

    // 掉落触发
    if (choice.lootChance) {
      if (Math.random() < choice.lootChance) {
        const loot = generateLootItem(raidState.distance + 500); // 奖励更好
        setRaidState(prev => ({ ...prev, tempLoot: [...prev.tempLoot, loot], currentLootItem: loot }));
        setScene('event');
        return; // 进入Loot界面
      }
    }

    // 默认回到Raid
    setScene('raid');
  };

  // ... (买卖逻辑与之前相同，省略部分重复代码，直接复用)
  const buyItem = (item) => {
    if (player.money >= item.cost) {
      setPlayer(prev => ({ ...prev, money: prev.money - item.cost, storage: [...prev.storage, { ...item, type: 'consumable' }] }));
      addLog(`购买了 ${item.name}`, 'success');
    } else { addLog('资金不足！', 'error'); }
  };
  const buyGear = (gear) => {
    if (player.money >= gear.cost) {
      setPlayer(prev => ({ ...prev, money: prev.money - gear.cost, [gear.type]: gear }));
      addLog(`装备了 ${gear.name}`, 'success');
    } else { addLog('资金不足！', 'error'); }
  };
  const sellItem = (index) => {
    const item = player.storage[index];
    if (!item) return;
    const sellPrice = item.val || Math.floor(item.cost / 2) || 1;
    // 遗物：招财猫效果
    const catRelic = player.relics.find(r => r.id === 'cat');
    const finalPrice = catRelic ? Math.floor(sellPrice * 1.2) : sellPrice;

    setPlayer(prev => ({ ...prev, money: prev.money + finalPrice, storage: prev.storage.filter((_, i) => i !== index) }));
    addLog(`出售 ${item.name}，获得 $${finalPrice}`, 'success');
  };
  const sellAllLoot = () => {
    const lootItems = player.storage.filter(i => i.type === 'loot');
    if (lootItems.length === 0) { addLog('没有可出售的战利品。'); return; }
    
    // 遗物：招财猫效果
    const catRelic = player.relics.find(r => r.id === 'cat');
    let totalVal = lootItems.reduce((acc, i) => acc + (i.val || 0), 0);
    if (catRelic) totalVal = Math.floor(totalVal * 1.2);

    setPlayer(prev => ({ ...prev, money: prev.money + totalVal, storage: prev.storage.filter(i => i.type !== 'loot') }));
    addLog(`一键出售杂物，获得 $${totalVal}`, 'success');
  };
  const useItem = (index) => {
    const item = player.storage[index];
    if (!item) return;
    
    // 装备遗物逻辑
    if (item.type === 'relic') {
       if (player.relics.some(r => r.id === item.id)) {
           addLog('已装备该遗物。'); return;
       }
       setPlayer(prev => ({
           ...prev,
           relics: [...prev.relics, item],
           storage: prev.storage.filter((_, i) => i !== index)
       }));
       addLog(`装备遗物：${item.name}`, 'success');
       return;
    }

    if (item.type !== 'consumable') return;

    let used = false;
    let newPlayer = { ...player };
    if (item.effect === 'heal' && player.hp < player.maxHp) { newPlayer.hp = Math.min(player.maxHp, player.hp + item.value); used = true; }
    else if (item.effect === 'satiety' && player.satiety < player.maxSatiety) { newPlayer.satiety = Math.min(player.maxSatiety, player.satiety + item.value); used = true; }
    else if (item.effect === 'mood' && player.mood < player.maxMood) { newPlayer.mood = Math.min(player.maxMood, player.mood + item.value); newPlayer.sanity = Math.max(0, player.sanity - 10); used = true; }
    else if (item.effect === 'sanity' && player.sanity < player.maxSanity) { newPlayer.sanity = Math.min(player.maxSanity, player.sanity + item.value); used = true; }
    else if (item.effect === 'buff_atk') { 
        // 简化的Buff逻辑，直接加到当前Raid状态，这里为了简单暂不实现复杂的临时buff
        addLog('Buff效果暂未实装', 'error'); 
        used = false; 
    }

    if (used) {
       newPlayer.storage = player.storage.filter((_, i) => i !== index);
       setPlayer(newPlayer);
       addLog(`使用了 ${item.name}。`, 'success');
    }
  };

  const startRaid = () => {
    setRaidState({
      distance: 0,
      dangerLevel: 1,
      currentEnemy: null,
      isGlitchEnemy: false,
      tempLoot: [],
      currentLootItem: null,
      currentInteractiveEvent: null,
    });
    setPlayer(p => ({ ...p, sanity: Math.max(0, p.sanity - 5) }));
    setScene('raid');
    addLog('进入废墟... 感觉到这里充满了恶意。');
  };

  const generateLootItem = (dist) => {
    const rand = Math.random() * 100;
    const luckBonus = Math.floor(dist / 100); 
    const moodBonus = player.mood > 80 ? 5 : 0;
    let targetRarity = 'white';
    if (dist > 3000 && Math.random() > 0.98) targetRarity = 'special';
    else {
        const score = rand + luckBonus + moodBonus;
        if (score > 140) targetRarity = 'gold';       
        else if (score > 115) targetRarity = 'purple';
        else if (score > 90) targetRarity = 'blue';
        else if (score > 60) targetRarity = 'green';
        else targetRarity = 'white';
    }
    let pool = LOOT_DB.filter(i => i.rarity === targetRarity);
    if (pool.length === 0) pool = LOOT_DB.filter(i => i.rarity === 'white');
    return pool[Math.floor(Math.random() * pool.length)];
  };

  const explore = () => {
    if (player.satiety <= 0) {
        addLog('你饿得走不动了... 生命值正在流失！', 'danger');
        setPlayer(p => ({ ...p, hp: Math.max(0, p.hp - 10) }));
        if (player.hp <= 10) setScene('gameover');
        return;
    }

    const newDist = raidState.distance + 100;
    const rng = Math.random();
    const currentDanger = 1 + Math.floor(newDist / 500);

    setPlayer(prev => ({
        ...prev,
        satiety: Math.max(0, prev.satiety - 5),
        sanity: Math.max(0, prev.sanity - 2),
    }));

    setRaidState(prev => ({ ...prev, distance: newDist, dangerLevel: currentDanger }));
    addLog(`深入废墟 ${newDist}m... (饱食-5, San-2)`);

    if (player.sanity < 50 && Math.random() > 0.7) addLog('你听到耳边有奇怪的低语...', 'danger');

    // 互动事件逻辑 (20% 概率)
    if (rng < 0.2) {
      const event = STORY_EVENTS[Math.floor(Math.random() * STORY_EVENTS.length)];
      setRaidState(prev => ({ ...prev, currentInteractiveEvent: event }));
      setScene('interactive_event');
      addLog('前方出现异常情况...', 'blue');
      return;
    }

    if (rng < 0.45) { // 提高一点遇敌率
      // 遭遇敌人逻辑
      let enemy = null;
      let isGlitch = false;
      if (player.sanity < 30 && Math.random() < 0.6) {
          isGlitch = true;
          const madnessScale = (50 - player.sanity) / 10;
          enemy = { name: '?&%#@!', hp: 50 + (madnessScale * 20), maxHp: 50 + (madnessScale * 20), atk: 8 + (madnessScale * 3), exp: 0 };
      } else {
          const enemyPool = ENEMIES.filter((_, idx) => idx < currentDanger);
          const enemyTemplate = enemyPool[Math.floor(Math.random() * enemyPool.length)] || ENEMIES[ENEMIES.length-1];
          enemy = { ...enemyTemplate, maxHp: enemyTemplate.hp };
      }
      setRaidState(prev => ({ ...prev, currentEnemy: enemy, isGlitchEnemy: isGlitch }));
      setPlayer(p => ({ ...p, sanity: Math.max(0, p.sanity - 5), mood: Math.max(0, p.mood - 2) }));
      setScene('combat');
      if (isGlitch) addLog('警告：遭遇不可名状的实体！', 'danger');
      else addLog(`遭遇敌对目标：${enemy.name}！`, 'danger');

    } else if (rng < 0.8) {
      // 发现物资
      const lootItem = generateLootItem(newDist);
      setRaidState(prev => ({ ...prev, tempLoot: [...prev.tempLoot, lootItem], currentLootItem: lootItem }));
      setPlayer(p => ({ ...p, mood: Math.min(p.maxMood, p.mood + 5) }));
      addLog(`发现物资：${lootItem.name}`, 'success');
      setScene('event');
    } else {
      setPlayer(p => ({ ...p, mood: Math.max(0, p.mood - 1) }));
      addLog('周围很安静，也许太安静了。');
    }
  };

  const handleCombat = (action) => {
    if (!raidState.currentEnemy) return;

    if (action === 'attack') {
      let hitChance = 0.9;
      let critChance = 0.1;
      let finalAtk = player.weapon.atk;

      // 遗物：肾上腺素
      const adrenalineRelic = player.relics.find(r => r.id === 'adrenaline');
      if (adrenalineRelic && player.hp < player.maxHp * 0.3) {
          finalAtk *= 2;
          addLog('肾上腺素激活！伤害翻倍！', 'blue');
      }

      if (player.mood > 80) { critChance = 0.3; }
      if (player.mood < 30) { hitChance = 0.6; critChance = 0; }

      if (raidState.isGlitchEnemy) {
          setPlayer(p => ({ ...p, satiety: Math.max(0, p.satiety - 2) }));
          addLog('攻击这个怪物让你感到异常疲惫...(饱食-2)', 'danger');
      }

      if (Math.random() > hitChance) {
          addLog('你的攻击落空了！(心情低落)', 'error');
      } else {
          let dmg = Math.max(1, finalAtk + Math.floor(Math.random() * 3));
          if (Math.random() < critChance) { dmg = Math.floor(dmg * 1.5); addLog('暴击！', 'success'); }

          const remainingEnemyHp = raidState.currentEnemy.hp - dmg;
          addLog(`你造成了 ${dmg} 点伤害。`);

          if (remainingEnemyHp <= 0) {
            addLog(`击败了敌人！`, 'success');
            
            // 遗物：吸血鬼之牙
            const vampireRelic = player.relics.find(r => r.id === 'vampire');
            if (vampireRelic) {
                setPlayer(p => ({ ...p, hp: Math.min(p.maxHp, p.hp + 5) }));
                addLog('吸血鬼之牙：汲取了 5 点生命。', 'blue');
            }

            setRaidState(prev => ({ ...prev, currentEnemy: null }));
            setScene('raid');
            return;
          }
          setRaidState(prev => ({ ...prev, currentEnemy: { ...prev.currentEnemy, hp: remainingEnemyHp } }));
      }

      // 敌人反击
      const enemyDmg = Math.max(0, raidState.currentEnemy.atk - player.armor.def);
      setPlayer(prev => ({ ...prev, hp: prev.hp - enemyDmg, mood: Math.max(0, prev.mood - 2) }));
      addLog(`敌人反击！受到 ${enemyDmg} 点伤害。`, 'danger');
      if (player.hp - enemyDmg <= 0) setScene('gameover');

    } else if (action === 'flee') {
       let fleeChance = 0.5;
       if (player.mood > 80) fleeChance = 0.7;
       if (player.mood < 30) fleeChance = 0.3;
       if (Math.random() < fleeChance) {
         addLog('逃跑成功！');
         setRaidState(prev => ({ ...prev, currentEnemy: null }));
         setScene('raid');
       } else {
         addLog('逃跑失败！被敌人追上了。', 'danger');
         const enemyDmg = Math.max(0, raidState.currentEnemy.atk - player.armor.def);
         setPlayer(prev => ({ ...prev, hp: prev.hp - enemyDmg }));
         if (player.hp - enemyDmg <= 0) setScene('gameover');
       }
    }
  };

  const evac = () => {
    const hasSpecial = raidState.tempLoot.some(i => i.rarity === 'special');
    
    // 设施：医疗站效果
    const healAmount = player.facilities.medical ? 40 : 20;

    setPlayer(prev => ({
      ...prev,
      hp: Math.min(prev.maxHp, prev.hp + healAmount),
      sanity: Math.min(prev.maxSanity, prev.sanity + 20),
      mood: Math.min(prev.maxMood, prev.mood + 20),
      storage: [...prev.storage, ...raidState.tempLoot]
    }));
    
    if (player.facilities.medical) addLog('医疗站为您提供了深度治疗。', 'blue');
    if (hasSpecial) addLog(`信号发射器已回收！`, 'success');
    addLog(`撤离成功！物资已转运至仓库。`, 'success');
    setScene('result');
  };

  const resetGame = () => {
    setPlayer({
        hp: 100, maxHp: 100, 
        satiety: 100, maxSatiety: 100,
        mood: 100, maxMood: 100,
        sanity: 100, maxSanity: 100,
        money: 200,
        weapon: GEAR.knife, armor: GEAR.clothes,
        relics: [], facilities: {},
        inventory: [], storage: [],
      });
      setScene('home');
      setLogs(['重新开始。祝你好运，行者。']);
  }

  // --- 渲染辅助 ---
  const CRTOverlay = () => {
      const glitchIntensity = player.sanity < 30 ? 'opacity-30' : 'opacity-0';
      return (
        <div className="pointer-events-none absolute inset-0 z-50 overflow-hidden rounded-lg">
            <div className="absolute inset-0 bg-[linear-gradient(rgba(0,0,0,0)_50%,rgba(0,0,0,0.2)_50%),linear-gradient(90deg,rgba(255,0,0,0.06),rgba(0,255,0,0.02),rgba(0,0,255,0.06))] bg-[length:100%_4px,3px_100%] pointer-events-none" />
            <div className="absolute inset-0 bg-[radial-gradient(circle_at_center,transparent_50%,rgba(0,0,0,0.4)_100%)] pointer-events-none" />
            <div className={`absolute inset-0 bg-noise mix-blend-overlay ${glitchIntensity} pointer-events-none transition-opacity duration-1000`}></div>
            {player.sanity < 50 && ( <div className="absolute top-2 left-2 text-[10px] text-red-500 animate-pulse font-bold tracking-widest">⚠ MENTAL CRITICAL</div> )}
        </div>
      );
  };

  return (
    <div className="min-h-screen bg-neutral-900 flex items-center justify-center p-4 font-mono text-slate-200 select-none">
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');
        .pixel-font { font-family: 'VT323', monospace; text-shadow: 0 0 2px rgba(0, 255, 0, 0.3); }
        .game-container { font-family: 'VT323', monospace; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .fade-in { animation: fadeIn 0.3s ease-out; }
        .bg-noise { background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E"); }
      `}</style>

      {/* 游戏容器 */}
      <div className="game-container relative w-full max-w-md bg-slate-800 rounded-2xl p-6 border-b-8 border-r-8 border-slate-950 shadow-2xl">
        
        {/* 顶部状态栏 */}
        <div className="mb-4 flex justify-between items-end border-b-4 border-slate-600 pb-2">
           <div>
             <h1 className="text-2xl text-yellow-500 leading-none mb-1 tracking-wider">废土行动</h1>
             <span className="text-base text-slate-400">EXTRACTION RPG</span>
           </div>
           <div className="text-right">
             <div className="text-green-400 text-xl flex items-center gap-1 justify-end">
                <span className="text-sm">$</span> {player.money}
             </div>
             <div className="text-lg text-slate-500">DAY {Math.floor(raidState.distance / 1000) + 1}</div>
           </div>
        </div>

        {/* 屏幕区域 */}
        <div className="relative bg-[#1a1c21] border-4 border-slate-700 rounded-lg min-h-[480px] flex flex-col justify-between overflow-hidden shadow-[inset_0_0_20px_rgba(0,0,0,0.8)]">
            <CRTOverlay />
            
            {/* 内容显示层 */}
            <div className="relative z-10 p-5 flex-1 flex flex-col">
                
                {/* 玩家多维状态条 */}
                <div className="bg-slate-800/80 p-3 rounded mb-4 border border-slate-600 backdrop-blur-sm grid grid-cols-2 gap-x-4 gap-y-1">
                    <div className="col-span-2 mb-1">
                         <div className="flex justify-between text-xs text-slate-400 mb-1">
                            <span>HP {player.hp}/{player.maxHp}</span>
                            <span className="flex gap-1">{player.relics.map((r,i) => <Gem key={i} size={10} className="text-purple-400"/>)}</span>
                         </div>
                         <ProgressBar current={player.hp} max={player.maxHp} color="bg-red-600" icon={<Heart size={10} className="text-red-500"/>} />
                    </div>
                    
                    <div>
                         <ProgressBar current={player.satiety} max={player.maxSatiety} color="bg-yellow-600" icon={<Utensils size={10} className="text-yellow-500"/>} />
                         <div className="flex justify-between text-[10px] text-slate-500 mt-0.5">
                            <span>饱食</span>
                            <span>{player.satiety}/{player.maxSatiety}</span>
                         </div>
                    </div>
                    <div>
                         <ProgressBar current={player.sanity} max={player.maxSanity} color="bg-blue-600" icon={<Activity size={10} className="text-blue-500"/>} />
                         <div className="flex justify-between text-[10px] text-slate-500 mt-0.5">
                            <span>理智</span>
                            <span>{player.sanity}/{player.maxSanity}</span>
                         </div>
                    </div>

                    <div className="col-span-2 mt-1">
                         <ProgressBar current={player.mood} max={player.maxMood} color="bg-purple-500" icon={<Smile size={10} className="text-purple-400"/>} />
                         <div className="flex justify-between text-[10px] text-slate-500 mt-0.5">
                            <span>心情</span>
                            <span>{player.mood}/{player.maxMood}</span>
                         </div>
                    </div>
                </div>

                {/* 场景渲染: 主页 */}
                {scene === 'home' && (
                  <div className="flex-1 flex flex-col items-center justify-center gap-4 text-center fade-in">
                    <div className="grid grid-cols-2 gap-4 w-full">
                        <PixelCard onClick={() => setScene('shop')}>
                            <div className="flex flex-col items-center py-2">
                                <ShoppingBag className="mb-2 text-yellow-500" size={24} />
                                <span className="text-xl">黑市交易</span>
                            </div>
                        </PixelCard>
                        <PixelCard onClick={() => setScene('hideout')}>
                            <div className="flex flex-col items-center py-2">
                                <Hammer className="mb-2 text-orange-500" size={24} />
                                <span className="text-xl">藏身处</span>
                            </div>
                        </PixelCard>
                        <PixelCard onClick={startRaid}>
                            <div className="flex flex-col items-center py-2">
                                <LogOut className="mb-2 text-red-500" size={24} />
                                <span className="text-xl">开始探索</span>
                            </div>
                        </PixelCard>
                        <PixelCard onClick={() => setScene('storage')}>
                           <div className="flex flex-col items-center py-2">
                                <Briefcase className="mb-2 text-blue-500" size={24} />
                                <span className="text-xl">物资仓库</span>
                            </div>
                        </PixelCard>
                    </div>
                  </div>
                )}

                {/* 场景渲染: 藏身处 (Hideout) */}
                {scene === 'hideout' && (
                  <div className="flex-1 flex flex-col fade-in overflow-y-auto no-scrollbar">
                    <h2 className="text-center text-xl text-orange-400 mb-4 border-b border-slate-700 pb-2">=== 设施升级 ===</h2>
                    
                    {/* 制造功能 */}
                    {player.facilities.workbench && (
                        <div className="bg-slate-800 p-3 mb-4 rounded border border-blue-500/50">
                            <h3 className="text-sm text-blue-400 mb-2">精密工作台</h3>
                            <button onClick={craftAmmo} className="w-full bg-slate-700 hover:bg-slate-600 text-sm py-2 rounded border border-slate-600">
                                制造弹药箱 ($50 + 1废钢)
                            </button>
                        </div>
                    )}

                    <div className="space-y-4">
                        {Object.entries(FACILITIES).map(([key, fac]) => {
                            const isBuilt = player.facilities[key];
                            return (
                                <div key={key} className={`p-3 border rounded ${isBuilt ? 'border-green-500/50 bg-green-900/10' : 'border-slate-600 bg-slate-800'}`}>
                                    <div className="flex justify-between items-center mb-1">
                                        <span className={`text-lg ${isBuilt ? 'text-green-400' : 'text-slate-200'}`}>{fac.name}</span>
                                        {isBuilt && <span className="text-xs bg-green-900 text-green-300 px-2 rounded">已建造</span>}
                                    </div>
                                    <p className="text-xs text-slate-400 mb-2">{fac.desc}</p>
                                    
                                    {!isBuilt && (
                                        <div className="mt-2">
                                            <div className="text-xs text-slate-500 mb-1">所需材料:</div>
                                            <div className="grid grid-cols-2 gap-1 mb-2">
                                                {Object.entries(fac.cost).map(([mat, count]) => {
                                                    const has = countItemInStorage(mat);
                                                    return (
                                                        <span key={mat} className={`text-xs ${has >= count ? 'text-green-500' : 'text-red-500'}`}>
                                                            {mat}: {has}/{count}
                                                        </span>
                                                    )
                                                })}
                                            </div>
                                            <button onClick={() => upgradeFacility(key)} className="w-full bg-orange-700 hover:bg-orange-600 text-white text-sm py-1 rounded">
                                                建造设施
                                            </button>
                                        </div>
                                    )}
                                </div>
                            );
                        })}
                    </div>
                    <button onClick={() => setScene('home')} className="w-full mt-4 bg-slate-700 p-2 text-lg hover:bg-slate-600 border border-slate-500 text-slate-300">返回</button>
                  </div>
                )}

                {/* 场景渲染: 互动事件 (Interactive Event) */}
                {scene === 'interactive_event' && raidState.currentInteractiveEvent && (
                    <div className="flex-1 flex flex-col justify-center text-center fade-in">
                        <div className="mb-6">
                            <HelpCircle size={64} className="mx-auto text-blue-400 mb-4 animate-bounce" />
                            <p className="text-lg text-slate-200">{raidState.currentInteractiveEvent.text}</p>
                        </div>
                        <div className="space-y-3">
                            {raidState.currentInteractiveEvent.choices.map(choice => (
                                <button key={choice.id} onClick={() => handleEventChoice(choice)} className="w-full bg-slate-800 hover:bg-slate-700 border border-slate-600 p-3 rounded text-left group">
                                    <span className="block text-blue-300 text-lg group-hover:text-blue-200">{choice.text}</span>
                                    {choice.req && <span className="block text-xs text-red-400 mt-1">需要: {choice.req.item ? ITEMS[choice.req.item]?.name || choice.req.item : `${choice.req.stat} ${choice.req.val}`}</span>}
                                </button>
                            ))}
                        </div>
                    </div>
                )}

                {/* ... (其他场景保持不变: storage, shop, raid, event, combat, result, gameover) */}
                {scene === 'storage' && (
                    <div className="flex-1 flex flex-col fade-in h-full overflow-hidden">
                        <div className="flex justify-between items-center border-b border-slate-700 pb-2 mb-2">
                            <h2 className="text-xl text-blue-400 tracking-widest">=== 仓库管理 ===</h2>
                            <button onClick={sellAllLoot} className="text-sm bg-red-900/50 text-red-300 px-2 py-1 rounded hover:bg-red-800 border border-red-700 flex items-center gap-1">
                                <Trash2 size={12} /> 一键卖杂物
                            </button>
                        </div>
                        <div className="flex-1 overflow-y-auto no-scrollbar space-y-2 pr-1">
                            {player.storage.length === 0 ? <div className="text-center text-slate-600 mt-10">仓库空空如也...</div> : 
                                player.storage.map((item, idx) => (
                                    <div key={idx} className={`p-2 border rounded flex justify-between items-center ${RARITY_CONFIG[item.rarity || 'white'].border} ${RARITY_CONFIG[item.rarity || 'white'].bg}`}>
                                        <div>
                                            <div className={`${RARITY_CONFIG[item.rarity || 'white'].color} text-lg`}>{item.name}</div>
                                            <div className="text-sm text-slate-400 flex gap-2">
                                                <span>{item.type === 'consumable' ? '消耗品' : item.type === 'relic' ? '遗物' : '物资'}</span>
                                            </div>
                                        </div>
                                        <div className="flex gap-2">
                                            {item.type === 'consumable' || item.type === 'relic' ? (
                                                <button onClick={() => useItem(idx)} className="bg-green-700 hover:bg-green-600 text-white px-2 py-1 text-sm rounded">{item.type === 'relic' ? '装备' : '使用'}</button>
                                            ) : (
                                                <button onClick={() => sellItem(idx)} className="bg-slate-700 hover:bg-slate-600 text-yellow-400 px-2 py-1 text-sm rounded border border-slate-600 flex items-center gap-1"><Coins size={12}/> ${item.val}</button>
                                            )}
                                        </div>
                                    </div>
                                ))
                            }
                        </div>
                        <button onClick={() => setScene('home')} className="w-full mt-4 bg-slate-700 p-2 text-lg hover:bg-slate-600 border border-slate-500 text-slate-300">返回</button>
                    </div>
                )}

                {scene === 'shop' && (
                    <div className="flex-1 overflow-y-auto no-scrollbar fade-in">
                        <div className="text-center mb-4 text-xl text-yellow-500 border-b border-slate-700 pb-2 tracking-widest">=== 黑市武器库 ===</div>
                        <div className="space-y-3">
                            <h3 className="text-sm text-slate-500 uppercase tracking-widest border-b border-slate-700/50 mt-4">生存补给</h3>
                            {Object.values(ITEMS).filter(i => i.cost > 0).map(item => (
                                <div key={item.id} onClick={() => buyItem(item)} className="group bg-slate-800/50 p-2 border border-slate-600 hover:bg-slate-700 hover:border-blue-600/50 cursor-pointer flex justify-between items-center rounded transition-colors">
                                    <div><div className="text-xl text-blue-400 group-hover:text-blue-300">{item.name}</div><div className="text-lg text-slate-500">{item.desc}</div></div>
                                    <div className="text-xl font-bold text-yellow-500">${item.cost}</div>
                                </div>
                            ))}
                            <h3 className="text-sm text-slate-500 uppercase tracking-widest border-b border-slate-700/50 mt-4">武器 & 护甲</h3>
                            {Object.values(GEAR).filter(g => g.cost > 0).map(item => (
                                <div key={item.id} onClick={() => buyGear(item)} className="group bg-slate-800/50 p-2 border border-slate-600 hover:bg-slate-700 hover:border-yellow-600/50 cursor-pointer flex justify-between items-center rounded transition-colors">
                                    <div><div className="text-xl text-green-400 group-hover:text-green-300">{item.name}</div><div className="text-lg text-slate-500">{item.desc}</div></div>
                                    <div className="text-xl font-bold text-yellow-500">${item.cost}</div>
                                </div>
                            ))}
                        </div>
                        <button onClick={() => setScene('home')} className="w-full mt-6 bg-slate-700 p-3 text-xl hover:bg-slate-600 border border-slate-500 text-slate-300">返回安全屋</button>
                    </div>
                )}

                {scene === 'raid' && (
                    <div className="flex-1 flex flex-col justify-between fade-in">
                        <div className="text-center space-y-4 mt-8">
                            <div className="relative inline-block"><Footprints className="mx-auto text-slate-600" size={48} /><div className="absolute top-0 right-0 animate-ping h-2 w-2 rounded-full bg-red-500 opacity-75"></div></div>
                            <div className="space-y-1"><div className="text-lg text-slate-500">正在搜索区域...</div><div className="text-4xl font-bold text-slate-200 tracking-widest">{raidState.distance}m</div></div>
                            <div className="flex justify-center gap-2 mt-2 bg-black/20 py-2"><span className="text-lg text-slate-500 mr-2">威胁等级:</span>{[...Array(raidState.dangerLevel)].map((_, i) => (<AlertTriangle key={i} size={20} className="text-red-500" />))}</div>
                        </div>
                        <div className="grid grid-cols-2 gap-4 mt-auto">
                             <PixelCard onClick={explore} className="bg-slate-800 hover:bg-green-900/20 border-green-800/50"><div className="text-center py-2"><span className="text-xl font-bold text-green-500 block mb-1">&gt; 继续搜寻</span><span className="text-lg text-slate-500">消耗5饱食/2San</span></div></PixelCard>
                             <PixelCard onClick={evac} className="bg-slate-800 hover:bg-blue-900/20 border-blue-800/50"><div className="text-center py-2"><span className="text-xl font-bold text-blue-500 block mb-1">&lt; 呼叫撤离</span><span className="text-lg text-slate-500">带回战利品</span></div></PixelCard>
                        </div>
                    </div>
                )}

                {scene === 'event' && raidState.currentLootItem && (
                     <div className="flex-1 flex flex-col items-center justify-center text-center fade-in">
                        <div className={`p-4 bg-slate-900 rounded-full mb-6 border-4 ${RARITY_CONFIG[raidState.currentLootItem.rarity].border} shadow-[0_0_20px_rgba(0,0,0,0.5)]`}>
                            {raidState.currentLootItem.rarity === 'special' ? <Radio size={56} className={`${RARITY_CONFIG[raidState.currentLootItem.rarity].color}`} /> : <Briefcase size={56} className={`${RARITY_CONFIG[raidState.currentLootItem.rarity].color}`} />}
                        </div>
                        <div className="mb-2 text-sm uppercase tracking-widest text-slate-500">{RARITY_CONFIG[raidState.currentLootItem.rarity].label} 物资</div>
                        <h2 className={`text-3xl mb-4 tracking-wide ${RARITY_CONFIG[raidState.currentLootItem.rarity].color}`}>{raidState.currentLootItem.name}</h2>
                        <div className="text-xl text-slate-300 mb-8 space-y-2"><p className="bg-slate-800 p-2 rounded border border-slate-600 inline-block px-4">估值: <span className="text-yellow-400 font-bold">${raidState.currentLootItem.val}</span></p></div>
                        <button onClick={() => setScene('raid')} className="w-full max-w-[200px] py-3 bg-slate-700 hover:bg-slate-600 text-xl rounded border-b-4 border-slate-900 active:border-b-0 active:translate-y-1 transition-all">收入背包</button>
                     </div>
                )}

                {scene === 'combat' && raidState.currentEnemy && (
                    <div className="flex-1 flex flex-col fade-in">
                         <div className="flex-1 flex flex-col items-center justify-center border-b-2 border-slate-700/50 border-dashed pb-6">
                            {raidState.isGlitchEnemy ? <div className="text-6xl mb-4 animate-pulse text-red-500 scale-110">?&%#</div> : <div className="text-6xl mb-4 grayscale hover:grayscale-0 transition-all duration-500 cursor-crosshair">👾</div>}
                            <div className="text-2xl text-red-500 font-bold mb-2 tracking-wide">{raidState.currentEnemy.name}</div>
                            <div className="w-full px-8">{raidState.isGlitchEnemy ? <div className="text-center text-red-600 font-bold text-xl animate-pulse">??? / ???</div> : <ProgressBar current={raidState.currentEnemy.hp} max={raidState.currentEnemy.maxHp} color="bg-purple-600" label="ENEMY" />}</div>
                            {!raidState.isGlitchEnemy && <div className="text-lg text-slate-500 mt-2 bg-black/30 px-3 rounded">ATK: <span className="text-red-400">{raidState.currentEnemy.atk}</span></div>}
                         </div>
                         <div className="mt-6 grid grid-cols-2 gap-4">
                            <PixelCard onClick={() => handleCombat('attack')} className="border-red-900/50 hover:bg-red-900/20 group"><div className="flex items-center justify-center gap-3 py-2"><Sword size={20} className="text-red-500 group-hover:rotate-45 transition-transform" /><div className="flex flex-col items-start"><span className="text-xl">攻击</span>{raidState.isGlitchEnemy && <span className="text-[10px] text-red-400">(消耗饱食)</span>}</div></div></PixelCard>
                            <PixelCard onClick={() => handleCombat('flee')} className="group"><div className="flex items-center justify-center gap-3 py-2"><Zap size={20} className="text-yellow-500 group-hover:-translate-x-1 transition-transform" /><span className="text-xl">逃跑</span></div></PixelCard>
                         </div>
                    </div>
                )}

                 {/* 场景渲染: 结算/死亡 */}
                 {(scene === 'result' || scene === 'gameover') && (
                     <div className="flex-1 flex flex-col items-center justify-center text-center fade-in">
                        {scene === 'gameover' ? (
                            <>
                                <Skull size={80} className="text-slate-700 mb-6" />
                                <h2 className="text-3xl text-red-600 mb-4 tracking-widest">行动失败</h2>
                                <p className="text-lg text-slate-400 mb-8">你在废土中倒下了。<br/>所有携带的物资都丢失了。</p>
                                <button onClick={resetGame} className="px-8 py-3 bg-red-900/30 border-2 border-red-800 text-red-400 text-xl rounded hover:bg-red-900/50 hover:text-red-200 transition-colors">重新开始</button>
                            </>
                        ) : (
                            <>
                                <Briefcase size={80} className="text-green-600 mb-6" />
                                <h2 className="text-3xl text-green-500 mb-4 tracking-widest">撤离成功</h2>
                                <p className="text-lg text-slate-400 mb-2">你带着战利品回到了安全屋。</p>
                                <div className="bg-black/20 p-4 rounded border border-slate-700 mb-8 max-h-40 overflow-y-auto w-full">
                                    <div className="text-sm text-slate-500 mb-2 uppercase border-b border-slate-600">获得物品</div>
                                    {raidState.tempLoot.map((item, i) => (<div key={i} className={`flex justify-between text-sm ${RARITY_CONFIG[item.rarity].color}`}><span>{item.name}</span><span>${item.val}</span></div>))}
                                    <div className="mt-2 pt-2 border-t border-slate-600 flex justify-between font-bold text-yellow-500"><span>总估值</span><span>${raidState.tempLoot.reduce((a,b)=>a+b.val, 0)}</span></div>
                                </div>
                                <button onClick={() => setScene('storage')} className="px-8 py-3 bg-blue-900/30 border-2 border-blue-800 text-blue-400 text-xl rounded hover:bg-blue-900/50 hover:text-blue-200 transition-colors">前往仓库整理</button>
                            </>
                        )}
                     </div>
                 )}

            </div>

            {/* 底部日志区域 */}
            <div className="h-36 bg-black p-3 overflow-y-auto font-mono text-sm md:text-base border-t-4 border-slate-700 z-10 no-scrollbar flex flex-col-reverse tracking-wide leading-snug">
                {logs.map((log, i) => (
                    <div key={i} className={`mb-1 border-l-2 pl-2 ${
                        log.includes('danger') || log.includes('受到') || log.includes('失败') || log.includes('缺少') ? 'text-red-500 border-red-900' : 
                        log.includes('success') || log.includes('获得') || log.includes('出售') || log.includes('建造') ? 'text-green-500 border-green-900' : 
                        log.includes('blue') ? 'text-blue-400 border-blue-900' :
                        'text-slate-500 border-slate-800'
                    }`}>
                        <span className="opacity-50 mr-2">{log.match(/\[(.*?)\]/)?.[0] || '>'}</span>
                        {log.replace(/\[.*?\] /, '').replace('danger', '').replace('success', '').replace('error', '').replace('blue', '')}
                    </div>
                ))}
            </div>
        </div>

        {/* 装饰性按钮 */}
        <div className="mt-6 flex justify-between items-center px-6 opacity-80">
             <div className="grid grid-cols-3 gap-1 w-24 h-24">
                <div className="bg-slate-700 rounded col-start-2 shadow-lg"></div>
                <div className="bg-slate-700 rounded col-start-1 row-start-2 shadow-lg"></div>
                <div className="bg-slate-800 rounded col-start-2 row-start-2 flex items-center justify-center"><div className="w-3 h-3 rounded-full bg-black/30"></div></div>
                <div className="bg-slate-700 rounded col-start-3 row-start-2 shadow-lg"></div>
                <div className="bg-slate-700 rounded col-start-2 row-start-3 shadow-lg"></div>
             </div>
             <div className="flex gap-6 transform rotate-12">
                 <div className="w-12 h-12 rounded-full bg-red-800 shadow-[0_4px_0_rgb(80,0,0)] border-t border-red-600"></div>
                 <div className="w-12 h-12 rounded-full bg-red-800 shadow-[0_4px_0_rgb(80,0,0)] border-t border-red-600"></div>
             </div>
        </div>

      </div>
    </div>
  );
}
